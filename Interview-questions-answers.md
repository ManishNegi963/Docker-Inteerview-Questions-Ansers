# Docker Interview Questions & Answers

- Difference between Virtual machine Vs Docker

  Docker and virtual machines (VMs) are both technologies used for virtualization, but they operate at different levels and serve different purposes. Here's a comparison between Docker and virtual machines:

### Docker:

1. **Containerization:**
   - Docker uses containerization technology to encapsulate applications and their dependencies into isolated containers.
   - Containers share the host OS kernel but run in isolated user spaces.

2. **Resource Efficiency:**
   - Containers are lightweight and share the host OS resources efficiently.
   - They have lower overhead compared to virtual machines.

3. **Isolation:**
   - Containers provide process-level isolation, meaning processes inside a container are isolated from the host and other containers.

4. **Speed:**
   - Containers can start and stop quickly, making them suitable for microservices architectures and dynamic scaling.

5. **Portability:**
   - Docker containers are highly portable, and the application and its dependencies are bundled together, ensuring consistent behavior across different environments.

6. **Use Case:**
   - Docker is often used for packaging and distributing applications with all their dependencies, making them easy to deploy and manage.

### Virtual Machines:

1. **Virtualization:**
   - VMs use hypervisors to create virtual instances of an entire operating system, including the kernel, on top of a physical host.

2. **Resource Overhead:**
   - VMs have more overhead compared to containers because each VM requires a full operating system.

3. **Isolation:**
   - VMs provide stronger isolation since each VM has its own full OS, which reduces the risk of security vulnerabilities.

4. **Speed:**
   - VMs typically have a longer start-up time compared to containers.

5. **Portability:**
   - VMs are less portable than containers because they encapsulate an entire operating system, making them larger and potentially more complex to manage.

6. **Use Case:**
   - VMs are often used for running multiple applications with different operating systems on a single physical host, consolidating resources and providing strong isolation.

### Choosing Between Docker and Virtual Machines:

- **Resource Efficiency vs. Isolation:**
  - Choose Docker if you prioritize resource efficiency and want lightweight, easily scalable containers.
  - Choose VMs if you need strong isolation with full OS virtualization.

- **Application Packaging and Deployment:**
  - Docker is excellent for packaging applications and their dependencies, ensuring consistency across different environments.
  - VMs are more suitable when you need to run multiple applications with different operating systems on the same host.

- **Speed and Agility:**
  - Docker is generally faster to start and stop, making it suitable for dynamic environments.
  - VMs may be preferable for more static environments with less frequent changes.

In practice, both Docker and VMs are often used together in a complementary way. Docker containers can run within VMs, providing an additional layer of abstraction and flexibility. The choice between Docker and VMs depends on the specific requirements and characteristics of the applications and infrastructure you are working with.

- What is Docker engine?

  Docker engine is a application to build, package and run containarized application with having all the code and dependencies and libraries needed to run the application in a isolated environment.

  Components of Docker engine.

    * Docker d (docker daemon) : It is a background process which manages the containers on high level and it manages the docker objects like images, volumes, container, network using container d on low level(code level: like executing the code in reference to manging the containers)
    
    * Docker CLI: It is a command line interface which allow user to interact with docker daemon and issue commands to manage image, container etc.
    
    * Container d: It manages the execution of container on low level, It handles the comlete lifecycle of creation, execution and destruction of containers. It manages the distribution of container images. This involves pulling container images from container registries (such as Docker Hub) and storing them locally.  

  
