Introducing any tool into a system is considered an increased security risk as a new tool means a new potential way into that system. These risks are amplified when dealing with a tool like Kubernetes, where you have a network of pods that can communicate with each other. The default setting allows any pod to communicate with another. This implies all kinds of security considerations. As a DevSecOps engineer, it is your responsibility to ensure these channels are secure.

Container hardening is the process of using container scanning tools to detect CVEs present in a cluster and remediate them to ensure minimal security breach risk.

# Checklist
## Pods

- Containers that run applications should not have root privileges
- Containers should have an immutable filesystem, meaning they cannot be altered or added to (depending on the purpose of the container, this may not be possible) 
- Container images should be frequently scanned for vulnerabilities or misconfigurations 
- <abbr title="Unrestricted policy, providing the widest possible level of permissions. This policy allows for known privilege escalations.">Privileged</abbr> containers should be prevented  
- [Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/) and [Pod Security Admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/)

## Network

- Access to the control plane node should be restricted using a firewall and role-based access control in an isolated network
- Control plane components should communicate using Transport Layer Security (TLS) certificates
- An explicit deny policy should be created
- Credentials and sensitive information should not be stored as plain text in configuration files. Instead, they should be encrypted and in Kubernetes secrets


## Authentication and Authorization

- Anonymous access should be disabled 
- Strong user authentication should be used 
- <abbr title="(Role-Based Access Control) - a method of granting access based on a role rather than an authenticated user identity.">RBAC</abbr> policies should be created for the various teams using the cluster and the service accounts utilized.


## Logging

Here are some logging best practices to ensure you know exactly what is going on in your cluster and can detect threats when they appear: 

- Audit logging should be enabled 
- A log monitoring and alerting system should be implemented

## Staying Secure

- Security patches and updates should be applied quickly
- Vulnerability scans and penetration tests should be done semi-regularly 
- Any obsolete components in the cluster should be removed