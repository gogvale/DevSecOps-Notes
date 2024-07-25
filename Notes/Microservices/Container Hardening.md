These are some ways to harden a docker container:
# Best Security Practices
## Update and Patch Regularly

Regularly update Docker software, host operating systems, and container images with the latest security patches and updates. This helps mitigate known vulnerabilities and ensures that your Docker environment is protected against potential exploits.

## Use Minimal Images

Utilize minimal and hardened base images for containers to minimize the attack surface. Remove unnecessary components and services from container images to reduce potential entry points for attackers. This practice also improves container performance and efficiency.

## [[Enforce Least Privilege]]

Run containers with the least privileges necessary for their intended functionality. Avoid using privileged containers unless absolutely required. Utilize Docker capabilities and security profiles (e.g., [[AppArmor]], SELinux, Seccomp) to restrict container capabilities and enforce security policies effectively.

## Secure Image Repositories

Implement access controls and authentication mechanisms for Docker image repositories (e.g., Docker Hub, private registries). Ensure that only authorized users and services can access and pull images from repositories. Verify the integrity and authenticity of images before deploying them in your environment.

## [[Regular Security Audits]]

Perform regular security audits and vulnerability assessments of Docker configurations, container deployments, and underlying infrastructure. Conduct penetration testing to identify and remediate potential security weaknesses before they can be exploited by attackers. Establish a proactive approach to security monitoring and incident response.
## Disable Docker Remote API (Expose Docker on Port 2375)

To enhance security, disable the Docker remote API if it's not required for your setup. By default, Docker listens on port 2375 for API connections, which can be a potential target for attackers. Modify the Docker daemon configuration (`/etc/docker/daemon.json`) to specify `"hosts": ["unix:///var/run/docker.sock"]`, ensuring Docker only listens on the Unix socket and not on TCP ports unless absolutely necessary. This prevents unauthorized access and reduces the attack surface.

## Use TLS Authentication and Encryption

Implement TLS (Transport Layer Security) for Docker API connections to secure communication between Docker clients and the Docker daemon. Generate and configure TLS certificates to authenticate clients and encrypt data transmitted over the network. This prevents eavesdropping, man-in-the-middle attacks, and unauthorized access to Docker resources via insecure channels.

## Implement Firewall Rules

Configure firewall rules to restrict access to Docker API ports (typically 2375 and 2376 for TLS) to trusted IP addresses or networks. Limiting access to these ports reduces exposure to potential attacks from unauthorized sources. Ensure firewall configurations are regularly reviewed and updated to reflect changes in network infrastructure or security policies.

## Use Docker Swarm or Kubernetes Instead

Consider leveraging Docker Swarm or Kubernetes for container orchestration instead of directly exposing Docker APIs. These platforms provide built-in security features such as network segmentation, role-based access control (RBAC), and secure API endpoints. They offer centralized management and monitoring capabilities that enhance container security and mitigate risks associated with direct Docker API exposure.

## Monitor Docker API Usage

Implement robust logging and monitoring of Docker API usage and connections. Monitor for unusual or unauthorized API calls, such as attempts to execute privileged commands or access sensitive resources. Establish alerts and response procedures to quickly detect and mitigate potential security incidents involving Docker containers.

## Protect Docker Daemon by creating a [[Docker context]]

Works like an SSH whitelist.
## Limiting the container resources usage

Assuming the machine becomes infected, a good second line of defense is limiting how much of the host a container can use by restricting it from cgroups:

| **Type of Resource** | **Argument**                                                  | **Example**                                 |
| -------------------- | ------------------------------------------------------------- | ------------------------------------------- |
| CPU                  | `--cpus` (in core count)                                      | `docker run -it --cpus="1" mycontainer`     |
| Memory               | `--memory` (in k, m, g for kilobytes, megabytes or gigabytes) | `docker run -it --memory="20m" mycontainer` |
You can also update this setting once the container is running. To do so, use the `docker update` command, the new memory value, and the container name. For example: `docker update --memory="40m" mycontainer`.

We can also inspect it by using [[Docker Cheat Sheet#View container information - docker inspect |docker inspect]].
