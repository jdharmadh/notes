### Operating Systems
- Protect important resources like memory
	- Applications should not use too much
	- Applications should not read other applications' memory
- Abstracts hardware details away for programmers
### The "Three Roles"
- **Referee**: enforce the rules, isolate, communicate
- **Illusionist**: give appearance of unlimited resources (virtualization, context switching)
- **Glue**: provide library functions for common tasks (IO, UI)
### The "Three Layers"
- **User Mode**: Apps, browsers, databases, libraries
- **Kernel Mode**: Scheduler, File System, TCP/IP, Device Drivers
- **Hardware Mode**: CPU, Disk, Network, Memory
### Challenges in Designing Operating Systems
OS code must be near perfect, even with buggy or malicious programs
- Reliability / Availability
- Portability
- Security
- Performance
- Adoption
