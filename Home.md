# Foundations

## [[DevSecOps Theory]]

[[DevOps]] is a set of tools and practices focused on cultural change to increase efficiency by uniting development and operations teams using integration and [[Intro to Pipeline Automation|automation]], and was created as a response to [[SDLC Methodologies#Agile|Agile]]'s drawbacks.

The main points of DevOps are:
- Developers can participate in the infrastructure using [[Infrastructure as Code|IaC]] with tools like Terraform and Vagrant
- [[Fundamentals of CI+CD|CI/CD]] allows for automatic deploy to multiple environments with minimal effort for making changes
- Organisations can scale vertically and horizontally as needed with [[Docker|containers]] and [[Kubernetes|orchestrators]]

DevSecOps integrates a Shifting Left posture, where security is the first concern on a project. This increases efficiency on the deployment and maintenance phases, reduces costs and makes it easier for auditing and monitoring.

Some of the challenges faced when implementing this cultural change on a company are **lack of understanding of shared responsibility** (security silos), **playing the blame game** (lack of visibility), and **losing development speed on CI/CD implementation** (stringent processes).

In order to make the integration seamless, we should **promote autonomy of teams** by making automated security tests routine and educating teams of the importance of security practices and team trust. Processes should be **visible and transparent** for everyone on the team and since no two teams are equal **flexibility and empathy should be imperative**.

## [[The CALMS Framework]]
The CALMS Framework is a tool for assessing a company's readiness to adopt a DevOps mindset, and it stands for **Culture, Automation, Lean, Measurement, and Sharing**

- **[[The CALMS Framework#Culture|Culture]]**: DevOps is all about teamwork and breaking down silos. It’s more about people working together than just following processes.
- **[[The CALMS Framework#Automation|Automation]]**: Automating tasks helps reduce manual work and makes everything run more smoothly and consistently.
- **[[The CALMS Framework#Lean|Lean]]**: Always look for ways to improve and learn from mistakes, moving quickly to deliver value without getting bogged down.
- **[[The CALMS Framework#Measurement|Measurement]]**: Keep track of key metrics to see what’s working and where things can get better, helping teams make informed decisions.
- **[[The CALMS Framework#Sharing|Sharing]]**: Sharing knowledge and responsibilities builds trust between teams, making everyone’s job easier and more effective.

[Source](https://www.atlassian.com/devops/frameworks/calms-framework)

## [[SSDLC]]

Secure [[SDLC Methodologies|SDLC]] means making security a top priority from the beginning for the same reasons DevSecOps is better than DevOps.

Examples of introducing security at all stages are:
 - architecture analysis during design,
 - code review and scanners during the development stage and 
 - conducting security assessments (e.g. penetration tests) before deployment.

The way we [[SSDLC#Implementation|implement]] it is by doing a **gap analysis** by checking the organization's current state, creating a **Software Security Initiative** by establishing goals and metrics for success, **formalize the process** by discussing it with the engineering team and finally, **investing in security training**.

The [[SSDLC#Processes|process]] goes as follows:
![[Phases of SSDLC.png]]


###  [[Risk Assessment]]
It refers to the likelihood of a threat being exploited impacting a resource or the target it affects.
We start by **imagining the worst case scenario** if the system is attacked, determine the **value of the data**, **how hard it is to attack it** and **how many users would be impacted**.

We may evaluate as low, medium or high by measuring `Risk = Severity x Likelihood` (qualitative) or on a scale of 1-25 according to [[5x5 Risk Matrix.png]] (quantitative).

### [[Threat Modeling]]
Threat modeling refers to frameworks for identifying security threats. It's like imagining what hackers might do to the application and figuring out how to stop them.

This is how we would implement these tools in a regular agile project:
1. **Kickoff and Planning:**
    - **[[Threat Modeling#PASTA|PASTA]] Stage 1 & 2:** Start by defining business objectives and technical scope with stakeholders.
2. **Design Phase:**
    - **STRIDE:** Apply the [[Threat Modeling#STRIDE|STRIDE]] model to identify potential security threats during the design phase.
3. **Threat Analysis:**
    - **PASTA Stage 3 & 4:** Break down the application and perform threat analysis.
    - **DREAD:** Use [[Threat Modeling#DREAD|DREAD]] to assess the risk of each threat identified with STRIDE.
4. **Vulnerability Analysis and Attack Simulation:**
    - **PASTA Stage 5 & 6:** Conduct vulnerability analysis and simulate attacks.
5. **Risk and Impact Assessment:**
    - **PASTA Stage 7:** Perform risk and impact analysis, incorporating DREAD ratings to prioritize threats.
6. **Mitigation Planning:**
    - Develop strategies to mitigate the highest risks based on your analysis.
### [[Code Scanning and Review]]
There are mainly two types of code review:
1. **Manual Review:** Experts go through the code line by line to spot issues.
2. **Automated Review:** Tools automatically scan the code to find vulnerabilities.
	- Early Development
		- [[Code Scanning and Review#Static Application Security Testing|SAST]]: Examining code without running it (static scanning)
		- [[Code Scanning and Review#SCA|SCA]]: Scan for vulnerabilities on imported libraries
	- Testing Phase
		- [[Code Scanning and Review#Dynamic Application Security Testing|DAST]]: Test code while application is running (sends multiple attacks)
		- [[Code Scanning and Review#IAST|IAST]]: Analyze code in real time while the application runs (embedded - monitors application execution)
	- Post-Deployment
		- [[Code Scanning and Review#RASP|RASP]]: Monitors and protects the application during runtime (can modify application's behavior if an attack is detected)

It's important to use both to save time but still being thorough in the evaluation.

### [[Security Assessments]]
Think of security assessments as health check-ups for your software. They help find and fix security issues before your software goes live, ensuring everything is safe and secure.

**Types of Assessments:**
1. **Vulnerability Assessment:**  
   - **What It Is:** A basic check-up that looks for potential security issues.
   - **How It Works:** Uses tools like OpenVAS and Nessus to scan for known problems and provides a report with severity ratings.
   - **Pros:** Quick, budget-friendly, and identifies many issues.
   - **Cons:** Can overwhelm with reports and doesn’t simulate real-world attacks.
2. **Penetration Testing:**  
   - **What It Is:** A deep dive that tries to exploit vulnerabilities to see how serious they are.
   - **How It Works:** Testers simulate attacks to see if they can break into the system and access sensitive info.
   - **Pros:** Reveals real-world risks, shows how vulnerabilities can be exploited, and offers detailed fixes.
   - **Cons:** Expensive, time-consuming, and might disrupt normal operations.
# Pipelines
[[Intro to Pipeline Automation|Pipeline automation]] **automates the building, testing, and deployment of software**, making the development process **faster** and **more reliable**. Key components include Continuous Integration (CI), which **merges and tests code from multiple developers**, and Continuous Delivery (CD), which **automates code deployment to various environments**. Automated testing ensures **code quality**, while deployment automation **speeds up releases**. The benefits are **efficiency, consistency, and better quality**, but it’s crucial to include security checks in the process.

In short, pipeline automation **helps deliver software updates quickly and reliably with a focus on maintaining quality and security**.
### [[Fundamentals of CI+CD|Fundamentals of CI/CD]]
GitLab outlines eight key principles for effective CI/CD:
1. **Single Source Repository**: Store all code and scripts in one place.
2. **Frequent Check-ins**: Regular, small code updates to the main branch for smoother integrations.
3. **Automated Builds**: Automatically build code as updates are pushed.
4. **Self-Testing Builds**: Automatically test builds for quality and security.
5. **Frequent Iterations**: Commit code regularly to reduce conflicts.
6. **Stable Testing Environments**: Test code in environments similar to production.
7. **Maximum Visibility**: Ensure all developers can access the latest code and builds.
8. **Predictable Deployments**: Streamline the pipeline for safe, anytime deployments.

### [[Fundamentals of CI+CD#A Typical CI/CD Pipeline|Typical CI/CD Pipeline]]

- **Developer Workstations**: Where developers write and build code.
- **Source Code Storage**: Central repository for tracking code versions (like GitLab).
- **Build Orchestrator**: Manages automation of builds and deployments (e.g., GitLab, Jenkins).
- **Build Agents**: Machines that build, test, and package the code (using GitLab runners, Jenkins agents).
- **Environments**: Stages like development, testing, and production where code is built and validated.

These fundamentals and pipeline components help streamline CI/CD processes, but it's essential to address security to avoid increasing the attack surface.

### [[Securing the Pipeline Checklist]]

1. **Pipeline Security is a Priority**: Ensuring the security of your CI/CD pipeline is crucial for safeguarding code and data integrity.
2. **Access Controls are Fundamental**: Restricting access to critical branches, environments, and CI/CD variables is the first line of defense against unauthorized changes and data exposure. 
3. **Runner Security is Essential**: Properly securing the machines running your GitLab Runner, along with strong authentication, is a must to prevent breaches.
4. **Secrets Management Matters**: Safeguarding sensitive data, such as API keys and passwords, through GitLab CI/CD variables with masking and secure variables is vital. Using environment variables is not enough.
5. **Isolate Environments**: Separating development (DEV) and production (PROD) environments minimizes the risk of compromising the latter through the former.
6. **Continuous Vigilance**: Regularly reviewing access permissions, scripts, and security configurations, combined with monitoring and alerting, ensures ongoing security.
7. **Education is Key**: Educating your team about security best practices is essential to maintaining a robust security posture.
8. **Secure the Build Process**: Implement isolation and containerization of builds, use least privilege access, and regularly update CI/CD tools to prevent attacks on the build process itself.
9. **Use Access Gates in Pipelines**: Incorporate checkpoints (access gates) within the pipeline to ensure that only code meeting quality and security standards progresses to the next stage.
# Microservices
Is a way of building software by breaking it down into small, independent services that each handle a specific function. These services communicate with each other through APIs.

**[[Docker]]:**  A tool that packages software into containers, which are portable units that include everything the software needs to run. Docker makes it easy to run microservices in different environments.

**[[Kubernetes]]:**  A platform that helps manage and scale containerized applications, like those built with Docker. It automates tasks like deployment and scaling, making it easier to manage multiple microservices.

# [[Infrastructure as Code]]

**Infrastructure as Code (IaC)** is a method for managing your IT infrastructure using code, just like you would with software. Instead of manually setting up servers and networks, you write scripts that automatically handle everything. IaC is a game-changer for automating and managing infrastructure, making your processes faster, more reliable, and easier to scale.

### [[Infrastructure as Code#Key Concepts and Benefits|Key Benefits]]
1. **Automation**: Cuts down on manual work and errors.
2. **Consistency**: Ensures identical setups every time.
3. **Version Control**: Track and manage changes easily.
4. **Scalability**: Adjust infrastructure as needed with minimal effort.
5. **Collaboration**: Teams work together more effectively using familiar coding practices.

### [[Infrastructure as Code#Tools and Technologies|Popular Tools]]
- **Terraform**
- **AWS CloudFormation**
- **Azure Resource Manager**
- **Ansible**

# [[Standards, policies, and regulations]]

**Standards** ensure uniformity and quality, **Policies** provide organizational guidelines and **Regulations** are legal requirements for compliance.

**Mexico:**
1. **LFPDPPP**: Protects personal data by requiring consent, data security measures, and breach notifications.
2. **NOM-151**: Sets rules for preserving digital documents and using electronic signatures.
3. **LPCI**: Safeguards critical information infrastructures with cybersecurity measures.
4. **LFTR**: Regulates telecoms, including data security and privacy.
5. **NOM-035**: Focuses on psychosocial risk factors at work, indirectly influencing security culture.
6. **LFPDPSO**: Similar to LFPDPPP but for public institutions, ensuring data privacy and transparency.
7. **FEA**: Governs advanced electronic signatures, ensuring security and legal recognition.
8. **NMX-I-27001**: Adapts ISO/IEC 27001 for managing information security in Mexico.
9. **LGTAIP**: Ensures transparency and data protection in public institutions.

**EU:**
1. **GDPR**: Regulates data protection with strong consent requirements, breach notifications, and user rights.

**United States:**
1. **HIPAA**: Protects patient health information with privacy, security, and breach notification rules.
2. **FISMA**: Establishes information security requirements for federal agencies.
3. **PCI DSS**: Sets security standards for credit card data, including encryption and access control.
4. **NIST Cybersecurity Framework**: Provides guidelines for managing cybersecurity risks with core functions: Identify, Protect, Detect, Respond, and Recover.
5. **SOX**: Requires financial reporting controls and IT system audits.
6. **GLBA**: Mandates privacy notices and data security for financial institutions.

**How to Apply These in DevSecOps:**
1. **Automate Compliance Checks**: Use tools to automate checks for compliance in CI/CD pipelines.
2. **Integrate Security Early**: Implement security practices early in the development process.
3. **Continuous Monitoring**: Employ monitoring tools to keep track of compliance and security.
4. **Regular Audits**: Conduct regular audits to ensure ongoing compliance.
5. **Documentation and Reporting**: Maintain detailed records of compliance efforts and report regularly.

Understanding and applying these standards helps ensure your software meets legal and security requirements efficiently.