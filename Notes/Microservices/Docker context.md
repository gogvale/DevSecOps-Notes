# Definition

Docker context is a way for your computer to know how to talk to different places where Docker is running. It's like having different profiles or setups for different Docker environments.
  
When you create a Docker context, you're setting up a specific configuration that tells Docker how to connect to a particular Docker environment, whether it's on your computer or somewhere else.

# Why It Matters

- **Simplifies Management**: Docker context makes it easier to switch between different Docker setups or environments without needing to remember complex connection details each time.

- **Enhances Security**: SSH ensures that when you manage Docker on remote servers, your commands and data are protected from unauthorized access or interception, maintaining the confidentiality and integrity of your Docker operations.

In essence, Docker context helps manage different Docker environments conveniently, while SSH ensures that this management is done securely over the internet.

Certainly! Let's walk through an example of configuring Docker context with SSH access:

# Example Configuration and Access

#### Setting Up Docker Context

1. **Creating Docker Context**:
   - Suppose you have a remote server where Docker is installed, and you want to manage Docker containers from your local computer.

   ```bash
   docker context create remote --docker "host=ssh://user@your-server-ip"
   ```

   - This command creates a Docker context named `remote` and configures it to connect to a remote Docker host using SSH. Replace `user` with your SSH username and `your-server-ip` with the IP address or hostname of your remote server.

2. **Switching Docker Context**:
   - After creating the context, switch to it to start using it for Docker commands.

   ```bash
   docker context use remote
   ```

   - Now, all Docker commands you run will interact with the Docker daemon running on your remote server.

#### SSH Access

3. **SSH Key-Based Authentication**:
   - Ensure you have SSH access to your remote server set up with key-based authentication for security.

   - If you haven't set up SSH keys, you can generate a new SSH key pair on your local computer:

     ```bash
     ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
     ```

   - Then, copy your public key (`~/.ssh/id_rsa.pub`) to your remote server's `~/.ssh/authorized_keys` file:

     ```bash
     ssh-copy-id user@your-server-ip
     ```

     Replace `user` and `your-server-ip` with your SSH username and server IP.

4. **Testing SSH Connection**:
   - Test the SSH connection to ensure it's working correctly:

     ```bash
     ssh user@your-server-ip
     ```

     This should log you into your remote server without prompting for a password, assuming SSH keys are set up correctly.

#### Using Docker Context with SSH

5. **Running Docker Commands**:
   - Now that your Docker context is set up and SSH connection verified, you can run Docker commands as usual, but they will be executed on your remote server:

     ```bash
     docker ps
     docker run -d nginx
     ```

     These commands will list running containers and start a new container running Nginx on your remote server.
# TLS Encryption

We can also interact with the docker daemon through HTTPS securely by accepting trusted devices only:

```shell
# Server
dockerd --tlsverify --tlscacert=myca.pem --tlscert=myserver-cert.pem --tlskey=myserver-key.pem -H=0.0.0.0:2376
```

```shell
# Client
docker --tlsverify --tlscacert=myca.pem --tlscert=client-cert.pem --tlskey=client-key.pem -H=SERVERIP:2376 info
```

| **Argument**  | **Description**                                                                                                                                                          |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `--tlscacert` | This argument specifies the certificate of the certificate authority. A certificate authority is a trusted entity that issues the certificates used to identify devices. |
| `--tlscert`   | This argument specifies the certificate that is used to identify the device.                                                                                             |
| `--tlskey`    | This argument specifies the private key that is used to decrypt the communication sent to the device.                                                                    |

# Conclusion

Configuring Docker context with SSH access allows you to manage Docker containers on remote servers securely and efficiently. It simplifies management by centralizing Docker configurations and enhances security through encrypted communication with SSH. This setup is particularly useful for deploying applications across different environments or managing Docker in cloud-based infrastructure.