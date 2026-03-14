# Strix Architecture and Workflow Analysis



## Overall Workflow

The complete workflow of the system can be understood as follows:

User → Strix CLI → AI Agents → Docker Sandbox Tools(Playwright,Nuclei) → Target Applications(JUICE SHOP-DOCKER via Ubuntu WSL,BOOKING APP-via Local System)
↓
LiteLLM Proxy → Azure GPT Model
↓
Langfuse Traces

---

## Step-by-Step Execution Flow

### 1. Starting the Scan

The scan begins when the user runs the Strix command from the terminal and provides the target URL.

Strix then initializes:

* Agent workflow
* Scan configuration
* Target scope
* Runtime sandbox environment

---

### 2. Reconnaissance Phase

In this phase, Strix tries to understand the attack surface of the application.

The Recon Agent performs tasks like:

* Crawling different pages
* Discovering API endpoints
* Identifying forms and input fields
* Collecting session cookies after login

Playwright is used heavily in this phase because both target applications contain dynamic UI flows such as login, booking, and feedback submission.

By automating browser actions, Playwright helps simulate real user behavior.

---

### 3. AI Reasoning Phase

After collecting information about endpoints and parameters, the agent sends this context to the language model through the LiteLLM proxy.

The model helps the agent decide:

* Which vulnerability to test next
* What payload to try
* Which tool should be used
* Whether deeper scanning is needed

This reasoning loop makes the scan adaptive instead of static.

---

### 4. Vulnerability Scanning Phase

The Vulnerability Agent executes different security tools.

**Nuclei** is used to run template-based checks for common issues such as:

* Cross-site scripting
* Missing security headers
* Open redirects
* Misconfigurations

**Playwright** is used for more complex attacks that require interaction with the UI, such as:

* Stored XSS validation
* Booking flow manipulation
* Authentication bypass testing
* CSRF exploitation

Session tokens collected during login are reused to simulate attacks from an authenticated user perspective.

---

### 5. Exploitation and Validation Phase

Once a possible vulnerability is detected, the Exploit Agent attempts to confirm it by sending crafted payloads.

Examples include:

* Injecting script payloads in input fields
* Modifying user IDs in booking requests
* Entering malicious redirect URLs
* Attempting directory traversal file access

The Validation Agent then checks whether the attack actually succeeded and collects proof such as:

* Response data
* Screenshot evidence
* Tool output logs

---

### 6. Observability and Trace Monitoring

All reasoning steps, tool executions, and decision points are captured in Langfuse.

This allows monitoring of:

* Token usage per agent step
* Execution latency
* Tool call sequence
* Decision-making paths

This information is useful for performance analysis and debugging failures.

---

### 7. Reporting Phase

After validation, the agents summarize confirmed vulnerabilities into structured findings.

The final output typically includes:

* Vulnerability type
* Affected endpoint
* Severity level
* Proof of concept
* Suggested remediation

Agents also summarize previous context to avoid excessive token usage.

---

## Session and Token Handling

During browser automation, authentication cookies and session tokens are captured.

These tokens are reused to:

* Test horizontal privilege escalation
* Perform stateful attack sequences
* Validate access control vulnerabilities

This enables realistic penetration testing scenarios.

---

## Parallel Execution Behavior

Strix uses a graph-based execution model which allows:

* Multiple endpoints to be scanned simultaneously
* Concurrent Nuclei template execution
* Parallel browser sessions
* Faster coverage of large applications

---

## Observed Architectural Dependency

The scan execution depends heavily on successful authentication with the LiteLLM proxy.

If the proxy token is not provisioned correctly:

* AI reasoning cannot start
* Tools are not triggered
* Scan workflow stops early

This indicates a need for better pre-scan health checks and fallback scanning strategies.

---

## Conclusion

Strix demonstrates a modern penetration testing architecture that combines AI-driven decision making with traditional security tools.

By integrating browser automation, template scanning, containerized execution, and observability tracking, the system enables intelligent and scalable vulnerability assessment workflows.
