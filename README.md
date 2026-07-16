# OWASP ZAP Security Scanner

A GitHub Actions-based security scanning pipeline using OWASP ZAP (Zed Attack Proxy) for automated web application security testing.

## Overview

This project automates security scanning of web applications using OWASP ZAP, a leading open-source security tool. The scanning is integrated into GitHub Actions, enabling continuous security testing on every push to the `main` branch or on-demand via manual workflow dispatch.

## Features

- **Automated Security Scanning**: Runs OWASP ZAP scans automatically on code pushes
- **HTTP/2 Support**: Includes a protocol upgrade script to force ZAP tools to use HTTP/2
- **Docker Integration**: Uses containerized ZAP for consistent scanning environments
- **Artifact Reporting**: Scan reports are automatically uploaded for review
- **Manual Trigger**: Run scans on-demand via GitHub Actions workflow dispatch

## Project Structure

```
.github/workflows/     GitHub Actions workflow definitions
http2.js              HTTP/2 protocol upgrade script for ZAP integration
zap.yml               OWASP ZAP configuration and scan parameters
README.md             This file
```

## Getting Started

### Prerequisites

- GitHub repository with Actions enabled
- Docker support (used by GitHub Actions)
- Target URL for security scanning

### Setup

1. **Clone or fork this repository**
   ```bash
   git clone https://github.com/Fabinwilfred/Test_Project.git
   cd Test_Project
   ```

2. **Configure the scan target**
   
   Edit `zap.yml` and update the target URL:
   ```yaml
   zap:
     target: "https://your-application-url.com"
   ```

3. **Commit and push changes**
   ```bash
   git add zap.yml
   git commit -m "Configure ZAP scan target"
   git push origin main
   ```

### Running the Scan

**Automatic (on push):**
- Any push to the `main` branch triggers the workflow automatically

**Manual (on-demand):**
1. Go to the **Actions** tab in your GitHub repository
2. Select **OWASP ZAP Scan** from the workflows list
3. Click **Run workflow**
4. Select the branch and click **Run workflow**

### Viewing Results

After the workflow completes:
1. Go to the **Actions** tab
2. Click on the completed workflow run
3. Download the **zap-report** artifact to review scan findings

## Configuration

### ZAP Configuration (`zap.yml`)

- **target**: The URL of the web application to scan
- **scan.level**: Scan intensity (Low, Medium, High)
- **scan.apiKey**: Optional API key for ZAP (if applicable)
- **context**: Define specific scanning contexts and URL patterns

### Workflow Configuration (`.github/workflows/main.yml`)

The workflow automatically:
- Checks out your repository code
- Pulls the latest OWASP ZAP Docker image
- Runs the configured security scan
- Uploads the scan report as a GitHub artifact

## HTTP/2 Upgrade Script

The `http2.js` script forces OWASP ZAP tools (spider, importers) to use HTTP/2 instead of HTTP/1.1. This is useful for:
- Testing HTTP/2-only applications
- Ensuring compatibility with modern protocols

**Note**: The target server must support HTTP/2, as there is no fallback to HTTP/1.1.

## Common Issues

**Scan fails with "server does not support HTTP/2"**
- Verify your target server supports HTTP/2
- Disable the HTTP/2 upgrade by removing the script from the ZAP configuration

**Permission denied errors**
- The workflow automatically sets up permissions with `chmod -R 777`

**No scan report generated**
- Check ZAP configuration in `zap.yml`
- Verify the target URL is accessible and responds to requests

## Security Considerations

- Keep your target URL and API keys secure
- Use GitHub Secrets to store sensitive configuration if needed
- Review scan reports regularly for security vulnerabilities
- This is a testing tool; always perform comprehensive security testing beyond automated scans

## Resources

- [OWASP ZAP Documentation](https://www.zaproxy.org/)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [ZAP Docker Image](https://ghcr.io/zaproxy/zaproxy)

## License

This project is provided as-is for security testing purposes.

## Contributing

Feel free to fork this repository and submit pull requests for improvements.

---

**Last Updated**: July 2026
