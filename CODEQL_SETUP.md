# GitHub CodeQL Analysis Setup Guide
## OpenMRS Core Security Scanning

This guide explains how to set up and use GitHub CodeQL for automated security analysis of the OpenMRS Core project.

## Overview

GitHub CodeQL is a semantic code analysis engine that can identify vulnerabilities and coding errors in your code. It's particularly powerful for Java applications and provides comprehensive security scanning capabilities.

## Prerequisites

1. **GitHub Repository**: Your OpenMRS Core code must be in a GitHub repository
2. **GitHub Actions**: Enabled on your repository
3. **CodeQL Access**: Available on GitHub (free for public repos, requires GitHub Advanced Security for private repos)

## Setup Instructions

### Step 1: Push Your Code to GitHub

If you haven't already, push your OpenMRS Core analysis to a GitHub repository:

```bash
# Initialize git repository (if not already done)
git init

# Add all files
git add .

# Commit your changes
git commit -m "Initial commit: OpenMRS Core 2.6.2 with CodeQL analysis"

# Add your GitHub repository as remote
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git

# Push to GitHub
git push -u origin main
```

### Step 2: Enable GitHub Actions

1. Go to your GitHub repository
2. Click on the "Actions" tab
3. Click "Enable Actions" if not already enabled

### Step 3: Configure CodeQL Analysis

The repository now includes:
- `.github/workflows/codeql-analysis.yml` - GitHub Actions workflow
- `.github/codeql/codeql-config.yml` - CodeQL configuration

### Step 4: Trigger Analysis

The analysis will automatically run when:
- You push to main/master branch
- You create a pull request
- Every Monday at 15:00 UTC (scheduled)

## Manual Trigger

To manually trigger CodeQL analysis:

1. Go to your repository on GitHub
2. Click "Actions" tab
3. Select "CodeQL Analysis" workflow
4. Click "Run workflow"
5. Select the branch and click "Run workflow"

## Viewing Results

### GitHub Security Tab

1. Go to your repository
2. Click "Security" tab
3. Click "Code scanning alerts"
4. View all detected vulnerabilities

### SARIF Output

The workflow generates SARIF files that can be:
- Downloaded from the Actions run
- Integrated with other security tools
- Used for compliance reporting

## Configuration Options

### Query Suites

The current configuration uses `security-and-quality` which includes:
- Security vulnerabilities
- Code quality issues
- Best practice violations

You can modify `.github/codeql/codeql-config.yml` to use different query suites:

```yaml
queries:
  - uses: security-extended  # More comprehensive security analysis
  - uses: security-and-quality  # Current setting
  - uses: security-experimental  # Experimental queries
```

### Custom Queries

You can add custom queries by creating a queries directory:

```yaml
queries:
  - uses: security-and-quality
  - uses: ./queries/custom-query.ql
```

### Path Filtering

Modify the paths in `codeql-config.yml` to focus on specific directories:

```yaml
paths:
  - 'api/**'  # Only analyze API code
  - 'web/**'  # Only analyze web code
```

## Integration with CI/CD

### Pull Request Integration

CodeQL analysis runs automatically on pull requests and:
- Shows results in the PR interface
- Blocks merging if critical vulnerabilities are found (if configured)
- Provides inline comments for detected issues

### Branch Protection

Set up branch protection rules to:
- Require CodeQL analysis to pass
- Block merging with security alerts
- Require security review

## Advanced Configuration

### Memory and Performance

For large repositories, you can optimize performance:

```yaml
# In codeql-analysis.yml
env:
  CODEQL_RAM: "6144"  # 6GB RAM
  CODEQL_THREADS: "4"  # 4 threads
```

### Custom Build Commands

If autobuild fails, specify custom build commands:

```yaml
- name: Build with Maven
  run: |
    mvn clean compile -DskipTests
    mvn package -DskipTests
```

## Troubleshooting

### Common Issues

1. **Build Failures**: Check if Maven build works locally
2. **Memory Issues**: Increase RAM allocation
3. **Timeout**: Increase workflow timeout limits
4. **False Positives**: Configure query filters

### Debug Mode

Enable debug logging by adding to workflow:

```yaml
env:
  ACTIONS_STEP_DEBUG: true
  ACTIONS_RUNNER_DEBUG: true
```

## Security Best Practices

1. **Regular Scanning**: Run analysis on every commit
2. **Review Alerts**: Regularly review and address security alerts
3. **False Positive Management**: Mark false positives as "used in tests" or "won't fix"
4. **Documentation**: Document security decisions and remediation plans

## Compliance and Reporting

### SARIF Export

Download SARIF files for:
- Compliance reporting
- Integration with security tools
- Audit trails

### Alert Management

Use GitHub's alert management features:
- Dismiss false positives
- Track remediation progress
- Generate compliance reports

## Next Steps

1. **Push your code to GitHub**
2. **Enable the workflow**
3. **Review initial results**
4. **Configure alerts and notifications**
5. **Set up branch protection rules**
6. **Integrate with your development workflow**

## Support

- [CodeQL Documentation](https://docs.github.com/en/code-security/code-scanning)
- [GitHub Advanced Security](https://docs.github.com/en/github/getting-started-with-github/learning-about-github/about-github-advanced-security)
- [CodeQL Query Help](https://codeql.github.com/docs/)

---

**Note**: This setup provides automated security analysis that complements your manual CodeQL assessment. The GitHub integration offers continuous monitoring and early detection of security issues. 