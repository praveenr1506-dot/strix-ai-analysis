## Runtime Failures Observed During Strix Scan

### 1. Sitemap Traversal Failure
Strix tried to automatically explore all pages of the target application but failed because it could not identify a valid root sitemap entry.  
This caused delay in deeper scanning since agents had to manually request specific endpoints.

### 2. LLM Connection Failures
Multiple scan attempts failed initially due to incorrect API key configuration and proxy authentication issues with LiteLLM.  
This stopped agents from reasoning and executing scan workflows.

### 3. Token Cache / Verification Issues
LiteLLM sometimes could not find the verification token in its cache/database.  
This resulted in authentication errors and scan interruptions.

### 4. LLM Proxy Gateway Failure (502 Bad Gateway)
At times, the LiteLLM proxy endpoint returned gateway errors which temporarily stopped agent reasoning and delayed the scan process.

### 5. Playwright Browser Automation Failure
The autonomous scan faced limitations in browser automation while testing the booking application. Playwright-based interaction was unable to consistently maintain authenticated session state and trigger deeper dynamic navigation flows. As a result, scan coverage remained limited and full vulnerability validation could not be completed.