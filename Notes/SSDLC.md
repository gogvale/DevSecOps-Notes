<abbr title="Secure Software Development Lifecycle">SSDLC</abbr> differs from [[SDLC Methodologies]] in making security a top priority from the beginning, and as explained in [[DevSecOps Theory#How does it differ from DevSecOps?]]. 
It mainly helps an organization by reducing costs and improving efficiency on the development and deployment stages.

![[Relative Cost of Fixing Defects.png]]
<small>Source: The research paper on the cost of identifying vulnerabilities can be found <a href="https://www.researchgate.net/profile/Maurice-Dawson/publication/255965523_Integrating_Software_Assurance_into_the_Software_Development_Life_Cycle_SDLC/links/02e7e52114e5e1ba71000000/Integrating-Software-Assurance-into-the-Software-Development-Life-Cycle-SDLC.pdf?origin=publication_detail">here</a>.
</small>

Examples of introducing security at all stages are:
 - architecture analysis during design,
 - code review and scanners during the development stage and 
 - conducting security assessments (e.g. penetration tests) before deployment.

# Implementation
﻿Like with every new process, understanding your gaps and state is critical for successfully introducing a new tool, solution, or change. To help grasp what your security posture is, you can start by doing the following:﻿

- Perform a **gap analysis** to determine what activities and policies exist in your organisation and how effective they are.
	- For example, ensuring policies are in place (what the team does) with security procedures (how the team executes those policies).  
- Create **Software Security Initiatives** (SSI) by establishing realistic and achievable goals with defined metrics for success. 
	- For example, this could be a Secure Coding Standard, playbooks for handling data, etc are tracked using project management tools.  
- **Formalize processes** for security activities within your SSI. 
	- After starting a program or standard, it is essential to spend an operational period helping engineers get familiarized with it and gather feedback before enforcing it. 
	- When performing a gap analysis, every policy should have defined procedures to make them effective.  
- **Invest in security training** for engineers as well as appropriate tools.
	- Ensure people are aware of new processes and the tools that will come with them to operationalize them, and invest in training early, ideally before establishing / onboarding the tool.

## Processes

![[Phases of SSDLC.png]]

- **[[Risk Assessment]] (how likely):**
    - **What it is:** Identifying potential security issues that could affect the application.
    - **Example:** Checking for risks like unauthorized access to customer accounts or data breaches.
- **[[Threat Modeling]] (potential damage):**
    - **What it is:** Imagining what hackers might do to the application and figuring out how to stop them.
    - **Example:** Identifying potential threats like someone trying to steal login credentials or exploit vulnerabilities to transfer money fraudulently.
- **[[Code Scanning and Review]] (development and deploy):**
    - **What it is:** Checking the code of the application to find and fix security problems.
    - **Example:** Reviewing the code to ensure there are no security flaws, such as SQL injection vulnerabilities or weak encryption methods.
- **[[Security Assessments]] (live application):**
    - **What it is:** Regularly monitoring and updating the application to keep it secure.
    - **Example:** Continuously updating the app to patch new security vulnerabilities and monitoring for suspicious activities.



