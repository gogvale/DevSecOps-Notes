Compliance and benchmarking are crucial aspects of securing assets, particularly containers in modern IT environments.
# Compliance

Compliance involves adhering to regulations and standards that ensure security best practices are followed. 

| **Compliance Framework** | **Description**                                                                                                                                                              | **URL**                                                                                                                  |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| NIST SP 800-190          | This framework outlines the potential security concerns associated with containers and provides recommendations for addressing these concerns.                               | [https://csrc.nist.gov/publications/detail/sp/800-190/final](https://csrc.nist.gov/publications/detail/sp/800-190/final) |
| ISO 27001                | This framework is an international standard for information security. The standard guides implementing, maintaining and improving an information security management system. | [https://www.iso.org/standard/27001](https://www.iso.org/standard/27001)                                                 |

Different industries may require adherence to specific regulatory frameworks; for instance, the healthcare sector must comply with HIPAA regulations for managing medical data securely.

# Benchmarking

Benchmarking, on the other hand, assesses an organization's adherence to these best practices. Tools such as [CIS Docker Benchmark]([https://www.cisecurity.org/benchmark/docker](https://www.cisecurity.org/benchmark/docker)), [OpenSCAP]([https://www.open-scap.org/](https://www.open-scap.org/)), [Docker Scout]([https://docs.docker.com/scout/](https://docs.docker.com/scout/)), [Anchore]([https://github.com/anchore/anchore-engine](https://github.com/anchore/anchore-engine), and [Grype]([https://github.com/anchore/grype](https://github.com/anchore/grype)) help organizations evaluate their containers against established security benchmarks like CIS Docker Benchmark and NIST SP-800-190. These tools identify vulnerabilities in Docker images, provide severity ratings (e.g., high, medium, low), and suggest fixes to mitigate risks effectively.

| **Benchmarking Tool** | **Description**                                                                                                                                                                                           |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CIS Docker Benchmark  | This tool can assess a container's compliance with the CIS Docker Benchmark framework.                                                                                                                    |
| OpenSCAP              | This tool can assess a container's compliance with multiple frameworks, including CIS Docker Benchmark, NIST SP-800-190 and more.                                                                         |
| Docker Scout          | This tool is a cloud-based service provided by Docker itself that scans Docker images and libraries for vulnerabilities. This tool lists the vulnerabilities present and provides steps to resolve these. |
| Anchore               | This tool can assess a container's compliance with multiple frameworks, including CIS Docker Benchmark, NIST SP-800-190 and more.                                                                         |
| Grype                 | This tool is a modern and fast vulnerability scanner for Docker images                                                                                                                                    |

---

Overall, compliance ensures that containers meet regulatory requirements, while benchmarking tools assess and enhance security posture by identifying and addressing vulnerabilities in containerized environments. These practices are essential for maintaining a secure and resilient IT infrastructure.