# CSN340_MCOSanncer_TESTING — MCP Security Research Samples

This folder contains three malicious MCP server datasets used for security scanning
experimentation in the CNDC course project.

## Datasets

### 1. damn-vulnerable-MCP-server
- **Source:** github.com/halencarjunior/damn-vulnerable-MCP-server
- **Description:** CTF-style MCP server with 10 intentionally vulnerable challenges
- **Attack types:** Prompt Injection, Tool Shadowing, Rug Pull, Hardcoded Secrets,
  Command Injection, Path Traversal
- **Tools exposed:** 31 tools across easy/medium/hard challenges

### 2. MCP-Artifact (Song et al.)
- **Source:** Academic PoC — Song et al.
- **Description:** Research artifact demonstrating semantic attacks against MCP clients
- **Attack types:** Tool Poisoning (RQ3/PoisonAttack), Indirect Prompt Injection
  (RQ3/MaliciousExternalResources), Malicious Supply Chain (RQ1)
- **Key files:** RQ3/Task*/PoisonAttack/weather_attack*.py

### 3. MCPSecBench (Yang et al.)
- **Source:** Academic benchmark — Yang et al.
- **Description:** MCP security benchmark covering system-level exploits
- **Attack types:** Command Injection (os.system), Path Traversal, Credential theft,
  Arbitrary code execution
- **Key files:** code/maliciousadd.py

## Scan Results Summary

| Sample | Snyk SCA | Snyk SAST | Cisco MCP Scanner (YARA) |
|---|---|---|---|
| damn-vulnerable-MCP-server | 0 CVE | 26 issues (3H/22M/1L) | 5/31 tools (16%) |
| Song et al. PoC | 3 HIGH CVE (mcp@1.8.1) | 71 issues (62H/2M/7L) | 0/5 tools (0%) |
| MCPSecBench | 0 CVE | 7 issues (0H/6M/1L) | 0/13 tools (0%) |

> Note: Cisco 16% detection in Sample 1 reflects trivial keyword patterns only.
> Against realistic semantic attacks (Samples 2 & 3), detection rate is 0%.

## Environment Setup

### Cisco MCP Scanner
```powershell
# Install
uv tool install --python 3.13 cisco-ai-mcp-scanner
$env:PATH = "C:\Users\<user>\.local\bin;$env:PATH"

# Scan via config
mcp-scanner --analyzers yara --format summary config --config-path mcp.json
```

### Snyk
```powershell
snyk test                 # SCA — dependency vulnerabilities
snyk code test            # SAST — source code analysis
```