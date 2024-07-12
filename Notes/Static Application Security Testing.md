# What is SAST? 
SAST is an automated security testing approach that analyzes source code without executing it. It scans code for vulnerabilities, coding errors, and security weaknesses.

# How Does SAST Work?

- **Parsing:** The SAST tool parses the source code to understand its structure and functionality.
- **Analysis:** The tool analyzes the code using various techniques like pattern matching and data flow analysis to identify potential vulnerabilities.
- **Reporting:** The tool generates reports highlighting vulnerabilities with details like severity, location in the code, and potential remediation steps.

# Limitations of SAST
- False positives: SAST tools might flag non-critical issues as vulnerabilities.
- Limited scope: May not detect all vulnerabilities, especially those depending on runtime behavior.
- Integration complexity: Integrating SAST tools into the development workflow can be challenging.

Using it along manual reviewing (automated to get most common ones out of the way and manual review for edge cases) is the most efficient way of doing things.

# Tools and Integrations
| Tool                                          | Pricing                                           | Supported Languages                                    | VSCode | JetBrains |
| --------------------------------------------- | ------------------------------------------------- | ------------------------------------------------------ | ------ | --------- |
| Fortify on Demand (Micro Focus)               | Freemium (limited features), Paid plans available | C/C++, Java, Python, .NET, COBOL                       | Yes    | Yes       |
| CodeScan (Veracode)                           | Freemium (limited scans), Paid plans available    | C/C++, Java, Python, .NET, JavaScript                  | Yes    | Yes       |
| Coverity (Synopsys)                           | Paid plans available                              | C/C++, Java, Python, C#, Ruby                          | Yes    | Yes       |
| HP CodeInspect (Micro Focus)                  | Paid plans available                              | C/C++, Java, Python, .NET, COBOL                       | Yes    | Yes       |
| Acunetix SAST                                 | Freemium (limited features), Paid plans available | C/C++, Java, Python, .NET, PHP                         | Yes    | Yes       |
| Fortify Static Code Analyzer (Micro Focus)    | Paid plans available                              | C/C++, Java, Python, .NET, COBOL                       | Yes    | Yes       |
| Brakeman (GitHub)                             | Free (Open Source)                                | Ruby                                                   | No     | No        |
| Cppcheck                                      | Free (Open Source)                                | C/C++                                                  | No     | No        |
| SonarQube                                     | Freemium (limited features), Paid plans available | Many languages (Java, C#, Python, JavaScript, etc.)    | Yes    | Yes       |
| RIPS (Ride Integrated Platform by GrammaTech) | Freemium (limited features), Paid plans available | C/C++, Java, Python, Ada, Fortran                      | No     | No        |
| Snyk Code                                     | Freemium, Paid plans available                    | JavaScript, TypeScript, Java, Python, PHP (and more)   | Yes    | Yes       |
| Semgrep                                       | Freemium, Paid plans available                    | Many languages (C/C++, Java, Python, JavaScript, etc.) | Yes    | Yes       |
| Psalm                                         | Free (Open Source)                                | PHP                                                    | Yes    | Yes       |
