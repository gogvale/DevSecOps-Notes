# Introduction  

Establishing a secure build environment is crucial to safeguarding your software development process against potential threats and vulnerabilities. In light of recent events such as the SolarWinds supply chain attack, it has become increasingly evident that building a robust security foundation is imperative. This note will explore key strategies to create a secure build environment, considering the lessons learned from the SolarWinds use case.

> [!Example] 
> See [[Insecure Design]] for an explanation about the SolarWinds case

---

# Pipeline Steps
## Source Code

The main problems with a incorrectly secured source code are:
* **Unauthorized Tampering** - only authorized users can modify the code
* **Unauthorized Disclosure** - protecting sensitive source code

In the room example, an employee (or an infected employee's computer) have full access to the company's repository and is able to scan the code looking for secret keys and credentials committed to git.

Some ways to prevent this from happening (in this case, for GitLab) are:

1. **Group-Based Access Control**: Organize projects into groups and set permissions at the group level for all projects within the group. This simplifies permission management and reduces errors.
2. **Access Levels** : Assign appropriate access levels (Guest, Reporter, Developer, Maintainer, Owner) to users or groups based on their needs.
3. **Sensitive Information Protection**:
	- Use `.gitignore` to exclude sensitive files like passwords from version control.
	- Use environment variables to store sensitive data securely, separate from code.
	- Enable branch protection to require code review and testing before merging changes.
4. **Maintain security with best practices:**
	- Regularly review and update access permissions.
	- Implement two-factor authentication (2FA) for user accounts.
	- Monitor audit logs to track access and modifications.
	- Regularly scan repositories for sensitive information. 

## Building Process
Source code usually relies on external libraries (dependencies). Hackers might try to inject malicious code into these dependencies (**supply chain attack**) or exploiting them to inject code into the build process (**dependency confusion attack**).

Pipelines involve remote code execution. If a hacker alters what's built or when, they could compromise our systems.

We need to ask ourselves three key questions:

1. **What actions trigger the build?**
	- By default, a commit triggers the build. We can configure it to only build on specific branches (e.g., main branch).
	- This allows more freedom for developers on other branches but requires stricter control over who can merge to the main branch.
	- Allowing builds on other branches or merge requests increases the attack surface.
2. **Who can trigger the build?**
	- If only commits to the main branch trigger the build, a small group of users approving merges would have control.
	- With builds from other actions (merge requests), we need to carefully limit who can perform those actions.
3. **Where will the build occur?**
	- We can have different build agents for different builds.
	- If multiple actions trigger builds, we might need to isolate them in separate environments.

**Remember:** By carefully considering these questions, we can minimize the attack surface of our build process.

In the room example we exploit the JenkinsFile to execute a reverse shell on the build server.

The best practices to secure the building step are:
1. **Isolation and Containerization**: Run builds in isolated containers to prevent interference and maintain consistency.
2. **Least Privilege**: Grant minimal permissions to CI/CD tools, restricting unnecessary access to sensitive resources.
3. **Secret Management**: Use CI/CD tools' secret management features to store and inject sensitive data securely.
4. **Immutable Artifacts**: Store build artifacts in a secure registry to prevent tampering and enable easy auditing.
5. **Dependency Scanning**: Integrate dependency scanning to identify and address vulnerabilities in third-party libraries.  
6. **Pipeline as Code**: Define CI/CD pipelines as code, version-controlled alongside the source code.  
7. **Regular Updates**: Keep CI/CD tools and dependencies up to date to address known vulnerabilities.
8. **Logging and Monitoring**: Monitor build logs for unusual activities and integrate them with security monitoring systems.
## Build Server

In this room, a hacker got access to Jenkins by login in with the default (mistakenly unchanged) credentials jenkins:jenkins, giving it privileged access.

The following steps can be followed to protect both your build server and build agents:  
1. **Build Agent Configuration**: Configure build agents to only communicate with the build server, avoiding external exposure.
2. **Private Network**: Place build agents within a private network, preventing direct internet access.
3. **Firewalls**: Employ firewalls to restrict incoming connections to necessary Build server-related traffic.
4. **VPN**: Use a VPN to access the build server and its agents securely from remote locations.
5. **Token-Based Authentication**: Utilize build agent tokens for authentication, adding an extra layer of security.
6. **SSH Keys**: For SSH-based build agents, use secure SSH keys for authentication.
7. **Continuous Monitoring**: Regularly monitor build agent activities and logs for unusual behavior.
8. **Regular Updates**: Update both the build server and agents with security patches.
9. **Security Audits**: Conduct periodic security audits to identify and address vulnerabilities.
10. **Remove Defaults and Harden Configuration:** Make sure to harden your build server and remove all default credentials and weak configurations.

## Pipeline

Even if we do everything correctly, we still have to consider that one of our developers may be compromised. Whether the actual developer is compromised through a social engineering attack or simply their credentials being exposed, this compromise could be the downfall of our pipeline and build. Fortunately, there are protections that can be applied!

### Access Gates

Access gates, also known as gates or checkpoints, serve as "stages" within a software development pipeline. They ensure that code progresses through the pipeline only after meeting predefined quality and security criteria. Access gates are crucial in enhancing the development process's _control_, _quality assurance_, and _security_. It's beneficial for everyone.

1. **Enhanced Control**: Access gates provide checkpoints in the pipeline, allowing controlled progression to different stages.
2. **Quality Control**: Gates ensures that code meets predefined quality standards before advancing.
3. **Security Checks**: Gates enables security assessments, such as vulnerability scans, before deployment.

﻿**Implementation Steps**:

1. **Manual Approvals**: Require manual approval before moving to the next stage, ensuring thorough reviews.
2. **Automated Tests**: Set up automated testing gates for code quality, unit tests, integration tests, etc.
3. **Security Scans**: Integrate security scanning tools to detect vulnerabilities in the codebase.
4. **Release Gates**: Use gates to verify proper documentation, versioning, and compliance.
5. **Environment Validation**: Validate the target environment's readiness before deployment.
6. **Rollback Plan**: Include a gate for a well-defined rollback plan in case of issues post-deployment.
7. **Monitoring**: Implement monitoring gates to assess post-deployment performance.
8. **Parallel Gates**: Run gates in parallel to expedite the pipeline without compromising quality.
9. **Auditing**: Regularly review gate configurations and results to ensure effectiveness.
## Environment

Protecting your build environment is crucial to prevent compromising your production pipeline through a single runner shared between DEV and PROD. Here are some steps you can take to enhance security:

**Isolate Environments**

Separate your DEV and PROD pipelines as much as possible. Use separate runners or runner tags for DEV and PROD builds. Ensuring that any compromise in the DEV environment does not directly impact PROD. This way, you can't compromise PROD in the way shown in this task.

**Restricted Access for CI/CD Jobs**

Limit access to the runner host. Only authorised personnel should have access to the machine(s) running the GitLab Runner. Implement strong access controls and monitor for unauthorised access. GitLab provides a "Protected CI/CD environments" feature that allows you to define access controls for environments, restricting who can deploy to them. Permission features limit and assigns who can modify CI/CD configuration, including the .gitlab-ci.yml file.

**Monitoring and Alerting**

Implement monitoring and alerting for your CI/CD pipeline and runner. Set up alerts for suspicious activity or failed builds, which could indicate a compromise. Review and audit access permissions periodically, especially for environments and CI/CD configurations. Revoke access for users or roles that no longer require it.
## Secrets
Protecting build secrets, even when using GitLab CI/CD variables, is crucial for maintaining the security of your pipelines. GitLab CI/CD provides a feature called "masked variables" to help prevent secrets from being exposed in logs. Here's how you can use this feature:

**Masking Variables**

You can mask variables in your .gitlab-ci.yml file by using the CI_JOB_TOKEN predefined variable. This token is automatically set by GitLab and can be used to mask any variable value you want to keep hidden.

For example, if you have a variable named MY_SECRET_KEY, you can use it like this:

```ansible
my_job:
  script:
    - echo "$MY_SECRET_KEY" # This will expose the secret
    - echo "masked: $CI_JOB_TOKEN" # This will mask the secret
```

**Use Secure Variables**

If you want to store secrets securely in GitLab, you can use GitLab CI/CD variables with the "Masked" option enabled. These variables are stored securely and are never exposed in job logs, even if you use them directly in your scripts. To create a secure variable:

- Go to the GitLab project.
- Navigate to Settings > CI/CD > Variables.
- Add a new variable, select the "Masked" checkbox, and provide the value.
- Once you've added a secure variable, you can use it in your .gitlab-ci.yml file without worrying about it being exposed in logs.

Note: Ensure that your job scripts do not inadvertently echo or print sensitive information, even when using masked variables. Double-check your scripts to avoid unintentional exposure of secrets.

**Access Control**

Limit access to CI/CD variables and logs. Only authorized can view job logs and variables in GitLab. You can configure project-level and group-level access controls to achieve this.