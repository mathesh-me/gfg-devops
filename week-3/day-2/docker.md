## Docker

### Why Docker is Fast?

- Docker uses the same kernel as the host machine. It doesn't need to create a new kernel for each container. This makes Docker lightweight and fast.
- If we run a command, it's just a process running on the host machine. It doesn't need to create a new kernel for each command.
- Docker Containers are just processes running on the host machine. They are not virtual machines. They are lightweight and fast.

---

## Namespaces

***Namespaces are a feature of the Linux kernel that partitions kernel resources such that one set of processes sees one set of resources while another set of processes sees a different set of resources.***

You can read more about namespaces [here](https://www.nginx.com/blog/what-are-namespaces-cgroups-how-do-they-work/).

---

## Kernel

- The kernel is the core of the operating system. It is responsible for managing the resources of the system and for communicating with the hardware.
- In simple words the kernel is the interface between the hardware and the software.
- The kernel is responsible for managing the resources of the system such as the CPU, the memory, the disk, etc.