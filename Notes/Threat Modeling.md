# Methodologies
## STRIDE
![[STRIDE.png]]
**What it is:**  
STRIDE is a model for identifying security threats. It stands for Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, and Elevation of Privilege.

**How to use it:**  
When you're looking at a new project, use STRIDE to think about different types of attacks that could happen. For example:

- **Spoofing:** Could someone pretend to be someone else?
- **Tampering:** Could someone change the data?
- **Repudiation:** Can someone deny their actions? (lack of evidence)
- **Information Disclosure:** Could data be exposed?
- **Denial of Service:** Could the service be made unavailable?
- **Elevation of Privilege:** Could someone gain higher access than they should?

**When to use it:**  
Use STRIDE during the design phase of a project to identify potential security threats early on.

## DREAD

**What it is:**  
DREAD is a model for assessing the risk of the threats you've identified. It stands for Damage, Reproducibility, Exploitability, Affected Users, and Discoverability.

**How to use it:**  
After identifying threats with STRIDE, use DREAD to rate each threat:

- **Damage:** How bad would an attack be?
- **Reproducibility:** How easy is it to reproduce the attack?
- **Exploitability:** How easy is it to launch the attack?
- **Affected Users:** How many people would be impacted?
- **Discoverability:** How easy is it to find the vulnerability?

**When to use it:**  
Use DREAD after identifying threats to prioritize them based on risk.

## PASTA
![[PASTA.png]]
**What it is:**  
PASTA (Process for Attack Simulation and Threat Analysis) is a risk-centric threat modeling methodology.

**How to use it:**  
PASTA involves seven stages:

1. **Define Objectives:** Understand the business objectives and security goals.
2. **Define the Technical Scope:** Look at the technical environment.
3. **Application Decomposition and Analysis:** Break down the application into its components.
4. **Threat Analysis:** Identify potential threats.
5. **Vulnerability Analysis:** Find vulnerabilities in the system.
6. **Attack Modeling:** Simulate potential attacks.
7. **Risk and Impact Analysis:** Assess the risk and impact of the identified threats and vulnerabilities.

**When to use it:**  
Use PASTA for comprehensive, detailed threat modeling, especially in complex environments.

# How to Use These in a New Project as a Consultant

1. **Kickoff and Planning:**
    - **PASTA Stage 1 & 2:** Start by defining business objectives and technical scope with stakeholders.
2. **Design Phase:**
    - **STRIDE:** Apply the STRIDE model to identify potential security threats during the design phase.
3. **Threat Analysis:**
    - **PASTA Stage 3 & 4:** Break down the application and perform threat analysis.
    - **DREAD:** Use DREAD to assess the risk of each threat identified with STRIDE.
4. **Vulnerability Analysis and Attack Simulation:**
    - **PASTA Stage 5 & 6:** Conduct vulnerability analysis and simulate attacks.
5. **Risk and Impact Assessment:**
    - **PASTA Stage 7:** Perform risk and impact analysis, incorporating DREAD ratings to prioritize threats.
6. **Mitigation Planning:**
    - Develop strategies to mitigate the highest risks based on your analysis.