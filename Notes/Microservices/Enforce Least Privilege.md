First, we need to understand what privileged containers are in this context. 
# Privileged Containers

Privileged containers are containers that have unchecked access to the host.
![[Pasted image 20240723140642.png]]

The entire point of containerization is to "isolate" a container from the host. By running Docker containers in "privileged" mode, the normal security mechanisms to isolate a container from the host are bypassed.
When running a Docker container in “privileged” mode, Docker will assign all possible <abbr title="Capabilities are a security feature of Linux that determines what processes can and cannot do on a granular level.">capabilities</abbr> to the container, meaning the container can do and access anything on the host (such as filesystems).

| **Capability**       | **Description**                                                                                                                                                                                 | **Use Case**                                                                                                                                                                              |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CAP_NET_BIND_SERVICE | This capability allows services to bind to ports, specifically those under 1024, which usually requires root privileges.                                                                        | Allowing a web server to bind on port 80 without root access.                                                                                                                             |
| CAP_SYS_ADMIN        | This capability provides a variety of administrative privileges, including being able to mount/unmount file systems, changing network settings, performing system reboots, shutdowns, and more. | You may find this capability in a process that automates administrative tasks. For example, modifying a user or starting/stopping a service.                                              |
| CAP_SYS_RESOURCE     | This capability allows a process to modify the maximum limit of resources available. For example, a process can use more memory or bandwidth.                                                   | This capability can control the number of resources a process can consume on a granular level. This can be either increasing the amount of resources or reducing the amount of resources. |

# Solution

It's recommended assigning capabilities to containers individually rather than running containers with the `--privileged` flag (which will assign all capabilities). For example, you can assign the `NET_BIND_SERVICE` capability to a container running a web server on port 80 by including the `--cap-add=NET_BIND_SERVICE` when running the container.

```shell
docker run -it --rm --cap-drop=ALL --cap-add=NET_BIND_SERVICE mywebserver
```

Finally, the command `capsh --print` can be used to determine what capabilities are assigned to a process.

![[Pasted image 20240723141052.png]]