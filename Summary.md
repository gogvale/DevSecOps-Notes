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

# Pipelines

# Scanning

# [[Microservices]]

# [[Infrastructure as Code]]

# [[Standards, policies, and regulations]]