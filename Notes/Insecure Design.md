# Definition

**Insecure design** refers to vulnerabilities which are inherent to the application's architecture. They are not vulnerabilities regarding bad implementations or configurations, but the idea behind the whole application (or a part of it) is flawed from the start.

# Example - SolarWinds supply chain attack

In the SolarWinds supply chain attack, hackers managed to breach SolarWinds, a major software provider. They inserted malicious code into the company's software updates for their Orion platform. This malicious code, known as SUNBURST or Solorigate, went unnoticed during SolarWinds' software development and distribution process.

Once customers, including government agencies and private companies, installed these compromised software updates, the malicious code allowed the attackers to gain unauthorized access to the networks of these organizations. Essentially, it acted as a backdoor, giving the hackers potential access to sensitive data and the ability to carry out further attacks.

The attack was significant because SolarWinds' software is widely used across various sectors, making the breach highly impactful. It exposed vulnerabilities in software supply chains and highlighted the importance of securing every step of the software development and distribution process to prevent such attacks.

# Helpful methods to prevent this from happening

## Patching

Since insecure design vulnerabilities are introduced at such an early stage in the development process, resolving them often requires rebuilding the vulnerable part of the application from the ground up and is usually harder to do than any other simple code-related vulnerability. 
The best approach to avoid such vulnerabilities is to **perform threat modelling at the early stages of the development lifecycle**.

## Set Up Appropriate Access Controls and Permissions

Limiting unauthorised access to the built environment is crucial for maintaining the integrity and security of the system. Following the principle of least privilege, grant access only to individuals or groups who require it to perform their specific tasks. Implement robust authentication mechanisms such as multi-factor authentication (MFA) and enforce strong password policies. Additionally, regularly review and update access controls to ensure that access privileges align with the principle of least privilege.

Implementing strict controls on privileged accounts is essential, including limiting the number of individuals with administrative access and strict monitoring and auditing mechanisms for privileged activities.

## Network Security  

Network security is vital in protecting the build system from external threats. Implementing appropriate network segmentation, such as dividing the built environment into separate network zones, can help contain potential breaches and limit lateral movement. Here are a few more essential points to consider:

- Implement secure communication channels for software updates and ensure that any third-party components or dependencies are obtained from trusted sources. 
- Regularly monitor and assess the security of your software suppliers to identify and address potential risks or vulnerabilities.

## Implement Isolation and Segmentation Techniques

By separating different stages of the build process and employing strict access controls, you can mitigate the risk of a single compromised component compromising the entire system. Isolation can be achieved through containerisation or virtualisation technologies, creating secure sandboxes to execute build processes without exposing the entire environment.