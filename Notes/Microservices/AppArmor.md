AppArmor prevents applications from performing unauthorized actions, however it works different from SELinux and Seccomp because it is not included in the application but in the operating system.

This mechanism is a Mandatory Access Control (MAC) system that determines the actions a process can execute based on a set of rules at the operating system level. To use AppArmor, we first need to ensure that it is installed on our system:

```shell
sudo aa-status
```

With the output "apparmor module is loaded", we can confirm that AppArmor is installed and enabled. To apply an AppArmor profile to our container, we need to do the following:

# Create an AppArmor profile

> [!NOTE] 
> There are tools out there that can help generate AppArmor profiles based on your Dockerfile.

Provided below is an example AppArmor profile (profile.json) for an "Apache" web server that:

- Can read files located in /var/www/, /etc/apache2/mime.types and /run/apache2. 
- Read & write to /var/log/apache2.
- Bind to a TCP socket for port 80 but not other ports or protocols such as UDP.
- Cannot read from directories such as /bin, /lib, /usr.

```json
/usr/sbin/httpd {

  capability setgid,
  capability setuid,

  /var/www/** r,
  /var/log/apache2/** rw,
  /etc/apache2/mime.types r,

  /run/apache2/apache2.pid rw,
  /run/apache2/*.sock rw,

  # Network access
  network tcp,

  # System logging
  /dev/log w,

  # Allow CGI execution
  /usr/bin/perl ix,

  # Deny access to everything else
  /** ix,
  deny /bin/**,
  deny /lib/**,
  deny /usr/**,
  deny /sbin/**
}
```
# Load the profile into AppArmor

```shell
sudo apparmor_parser -r -W /home/cmnatic/container1/apparmor/profile.json
```

# Run our container with the new profile

```shell
docker run --rm -it --security-opt \
apparmor=/home/cmnatic/container1/apparmor/profile.json mycontainer
```

Just like Seccomp, Docker already applies a default AppArmor profile at runtime. However, this may not be suitable for your specific use case, especially if you wish to harden the container further while maintaining functionality. You can learn more about using AppArmor with Docker [here](https://docs.docker.com/engine/security/apparmor/).