# Autonomous AI Penetration Testing Analysis using Strix

## Overview

This project demonstrates practical analysis and execution of autonomous penetration testing workflows using the Strix AI agent framework. The assessment focused on understanding multi-agent security scanning architecture, runtime behavior, vulnerability validation, and observability integration.

Two target applications were considered:

* OWASP Juice Shop (intentionally vulnerable web application)
* Custom Slot Booking Application (authentication-based workflow)

---

## Objectives

* Understand agent-based penetration testing architecture
* Execute autonomous scans and analyse vulnerability findings
* Study runtime failures and scanning limitations
* Attempt observability integration using Langfuse
* Provide improvement recommendations for autonomous security tooling

---

## Agent Workflow Understanding

Strix uses a multi-agent system where different agents collaborate during the scan lifecycle:

* **Recon Agent** discovers endpoints and input parameters
* **Mapping Agent** builds structured attack surface context
* **Vulnerability Agent** performs payload testing and template-based scanning
* **Exploitation Agent** validates suspected vulnerabilities
* **Reporting Agent** generates structured vulnerability outputs

Agent reasoning decisions are driven by LLM responses routed through a proxy gateway.

---

## Key Findings

### Juice Shop

The autonomous scan identified high-risk vulnerabilities including client-side injection and information disclosure indicators. Manual validation confirmed that certain findings were exploitable while others required deeper contextual verification.

### Booking Application

Complete vulnerability assessment could not be achieved due to browser automation limitations during authenticated workflow exploration. Dynamic navigation and session persistence challenges reduced scan coverage.

---

## Runtime Observations

* Limited crawling depth in authentication-dependent flows
* Browser automation constraints affecting stateful testing
* Environment configuration challenges during observability setup
* Telemetry traces not captured despite Langfuse configuration attempts

These observations highlight real-world challenges in autonomous penetration testing environments.

---

## Langfuse Observability Attempt

Langfuse was configured using environment variables to monitor LLM reasoning traces and agent execution metrics. Although scans executed successfully, telemetry data was not consistently visible in the dashboard even after sandbox rebuild and configuration retries.

This demonstrates the importance of reliable observability pipelines in AI-driven security workflows.

---

## Suggested Improvements

* Enhance stateful browser automation handling
* Improve authenticated crawling strategies
* Reduce false positives through stronger validation logic
* Provide clearer telemetry configuration workflows
* Add retry and fallback mechanisms for runtime stability

---

## Skills Demonstrated

* Autonomous security scanning analysis
* OWASP vulnerability understanding
* Docker sandbox execution and debugging
* LLM proxy configuration and troubleshooting
* Observability integration concepts
* Runtime failure analysis and documentation

---

## Conclusion

This project provided hands-on experience in analysing AI-driven penetration testing systems. It highlights both the capabilities and practical limitations of autonomous security agents when applied to modern web applications. The learning outcomes contribute to deeper understanding of secure system assessment and intelligent automation in cybersecurity.
