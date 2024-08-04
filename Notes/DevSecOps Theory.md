# What Is [[DevOps]]?

DevOps is a set of practices, tools, and a cultural philosophy that automate and integrate the processes to build software. It was created as a response against the drawbacks of Agile (see [[SDLC Methodologies]] for more info).

DevOps is quite different from the previous methodologies because it focuses on driving "cultural change" to increase efficiency. It does this by uniting the magic of all teams working on a project, using integration and automation.
## In Summary:

- Developers can provide resources to public clouds without depending on IT to provision infrastructure
- Continuous integration and deployment (CI/CD) processes automatically set up testing, staging, and production environments in the cloud or on-premises. They can be decommissioned, scaled, or re-configured as needed.  
- Infrastructure-as-Code (IaC) is widely used to deploy environments declaratively, using tools like Terraform and Vagrant.
- Organisations can now provision containerised workloads dynamically using automated, adaptive processes

Read more at: [https://www.appknox.com/blog/history-of-devops](https://www.appknox.com/blog/history-of-devops)

# How is DevSecOps different?

DevSecOps differs from traditional DevOps by setting a Shifting Left posture - where security is the first concern on a new project. 
By doing this, it helps bring down vulnerabilities, maximises test coverage, and intensifies the automation of security frameworks. This reduces risk massively, assisting organisations in preventing brand reputation damage, and economic losses due to security flaws incidents, making life easier for auditing and monitoring.

![[Shifting Left.png]]

Culture is key. It does not work without **open communication** and **trust**. It only works with collective effort. DevSecOps should aim to bridge the security knowledge gaps between teams; for everyone to think and be accountable for security, they first need the tools and knowledge to drive this autonomy efficiently and confidently.

## Challenges

### Security Silos

When the organization doesn't understand that culture is key, the security role is delegated to a person or team and efficiency decreases or halts completely
### Lack of visibility and Prioritisation

Again, lack of culture - developers and QA should be involved in the security part and work as a team to patch vulnerabilities instead of playing the blame game
### Stringent Processes

Security shouldn't be a burden to developers when doing their work - an appropriate sandbox environment with fake data and minimal security blocks should be used, and leave the pipeline tests be used on environments with real or semi-real data in favor of development speed

## Culture

### Promote Autonomy of Teams  
Encourage team independence by automating security processes within the development pipeline, making security tests routine. Lead by example and educate teams through playbooks/runbooks. Build trust and overlap in knowledge between teams to compensate for the limited number of security engineers.

### Visibility and Transparency  
Ensure every tool has a process that provides visibility and promotes transparency. Teams need to see the security state of their services, such as through a dashboard displaying security flaws. Tools should be accessible and explain issues clearly to promote education and autonomy.

### Flexibility Through Understanding and Empathy  
Understand the different perspectives on risk between security and other teams. Tailor processes to fit how developers work and what they prioritize. Building processes that are flexible and empathetic to the team’s needs increases the chances of successful security integration.