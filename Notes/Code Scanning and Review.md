# Why It Matters
Secure code review and analysis are crucial to ensure web applications are free from vulnerabilities that could be exploited by attackers.

# Types of Code Review

1. **Manual Review:** Experts go through the code line by line to spot issues.
2. **Automated Review:** Tools automatically scan the code to find vulnerabilities.

# Types of Code Analysis

## <abbr title="Static Application Security Testing">SAST</abbr> (Static Application Security Testing)
 
   - Examines code without running it.
   - Finds bugs before the application goes live.
   - Integrates into early development.
   - **Common Tools:** Checkmarx, Veracode, Fortify, SonarQube

## <abbr title="Dynamic Application Security Testing">DAST</abbr> (Dynamic Application Security Testing)

   - Tests code while the application is running.
   - Simulates attacks to find vulnerabilities.
   - Typically used in the testing phase.
   - **Common Tools:** [[OWASP-ZAP]], Burp Suite, AppSpider, Acunetix

## <abbr title="Interactive Application Security Testing">IAST</abbr> (Interactive Application Security Testing)

   - Analyzes code in real-time while the application runs.
   - Combines <abbr title="Static Application Security Testing">SAST</abbr> and <abbr title="Dynamic Application Security Testing">DAST</abbr> features.
   - Identifies issues during staging or testing.
   - **Common Tools:** Contrast Security, Seeker by Synopsys, Veracode IAST

## <abbr title="Software Composition Analysis">SCA</abbr> (Software Composition Analysis)

   - Scans for vulnerabilities in open-source components.
   - Helps track and manage open-source usage.
   - **Common Tools:** Black Duck, Snyk, WhiteSource, Dependency-Check

## <abbr title="Runtime Application Self Protection">RASP</abbr> (Runtime Application Self Protection)

   - Monitors and protects the application during runtime.
   - Blocks suspicious activity and alerts security teams.
   - **Common Tools:** Contrast Security, Signal Sciences, Imperva RASP

# Choosing Tools
Combining <abbr title="Static Application Security Testing">SAST</abbr>, <abbr title="Dynamic Application Security Testing">DAST</abbr>, and <abbr title="Interactive Application Security Testing">IAST</abbr> provides comprehensive coverage. Each tool serves a specific stage in the development cycle, from early coding to post-deployment monitoring. Using multiple tools ensures thorough security and compliance with standards.

# Timeline of Implementation

- **Early Development:** Use <abbr title="Static Application Security Testing">SAST</abbr> and <abbr title="Software Composition Analysis">SCA</abbr>.
- **Testing Phase:** Use <abbr title="Dynamic Application Security Testing">DAST</abbr> and <abbr title="Interactive Application Security Testing">IAST</abbr>.
- **Post-Deployment:** Use <abbr title="Runtime Application Self Protection">RASP</abbr> for ongoing protection.