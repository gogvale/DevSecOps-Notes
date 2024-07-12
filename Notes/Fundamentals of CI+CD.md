According to [Gitlab](https://about.gitlab.com/topics/ci-cd/), there are eight fundamentals for CI/CD:

- **A single source repository** - Source code management should be used to store all the necessary files and scripts required to build the application.  
- **Frequent check-ins to the main branch** - Code updates should be kept smaller and performed more frequently to ensure integrations occur as efficiently as possible.  
- **Automated builds** - Build should be automated and executed as updates are being pushed to the branches of the source code storage solution.  
- **Self-testing builds** - As builds are automated, there should be steps introduced where the outcome of the build is automatically tested for integrity, quality, and security compliance.  
- **Frequent iterations** - By making frequent commits, conflicts occur less frequently. Hence, commits should be kept smaller and made regularly.  
- **Stable testing environments** - Code should be tested in an environment that mimics production as closely as possible.  
- **Maximum visibility** - Each developer should have access to the latest builds and code to understand and see the changes that have been made.  
- **Predictable deployments anytime** - The pipeline should be streamlined to ensure that deployments can be made at any time with almost no risk to production stability.

While all of these fundamentals will help to ensure that CI/CD can streamline the DevOps process, none of these really focus on ensuring that the automation does not increase the attack surface or make the pipeline vulnerable to attacks.

## A Typical CI/CD Pipeline

![[Typical Pipeline.png]]
- **Developer workstations** - Where the coding magic happens, developers craft and build code. In this network, this is simulated through your AttackBox.  
- **Source code storage solution** - This is a central placeholder to store and track different code versions. This is the Gitlab server found in our network.  
- **Build orchestrator** - Coordinates and manages the automation of the build and deployment environments. Both Gitlab and Jenkins are used as build servers in this network.  
- **Build agents** - These machines build, test and package the code. We are using GitLab runners and Jenkins agents for our build agents.  
- **Environments** - Briefly mentioned above, there are typically environments for development, testing (staging) and production (live code). The code is built and validated through the stages. In our network, we have both a DEV and PROD environment.  