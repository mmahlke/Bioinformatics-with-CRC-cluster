# **Bioinformatics with Pitt's Center for Research Computing (CRC) cluster**
*YNA lab training series, pt 1*



## What is the cluster?
![Image depicting accessing the cluster from your computer.](https://crc-pages.pitt.edu/user-manual/_assets/img/getting-started/getting-started-map.png)
*Image from CRC user manual*

The 'cluster' refers to the **CRC ecosystem** that contains the total footprint of the CRC infrastructure, including high performance computing clusters, data storage systems, networking equipment, and software. For us, we can simply imagine it as a giant, stronger, faster computer. 

Why are we using it? A typical laptop or personal computer does not have enough storage space or resources (Memory, Processing power) to analyse many sequencing files. For example, a small sequenicng file like a CUT&RUN experiment starts off as 3 Gb and a large sequencing file like a DiMeLo-seq experiment can be around 20 Gb when compressed. The storage footprint of sequencing files can double or triple during analysis.

We conenct to the CRC cluster through our **Client**, which is the software we are using on our personal computer to interact with the CRC cluster. Our interactions with the cluster pass through an **Access Portal**, or a remote server that take the information we submit from our client and passes it on to the CRC cluster. **Access portals** are typically remote servers, which refers to a computer system that is accessed over a network, like the internet, allowing users to store, manage, and access data and applications from anywhere with an internet connection, rather than being physically located in the same place as the user.

For us, our **client(s)** are Pitt's VPN software, which gives us access to Pitt's secure private network, and our terminal emulator software (MobaXterm or Termius), which allows us to establish a connection to the CRC. Why is it called a terminal emulator? Take yourself way back in your imagination to when computers were huge and took up an entire room. The box that controlled the computer was called the terminal. Here, the terminal emulator is serving the same function for the CRC cluster, but instead of being connected to the giant computer (cluster), it's giving commands to the giant computer over the internet. 

Our **access portal** refers to how we are interacting with the cluster. We will primarily interact through the 'login node' pictured above. CRC also provides user access to viz (in-browser Linux Desktop environment on the CRCD system), OnDemand (requesting resources for interactive visual software, etc) and JupyterHub (web-based interactive development environment for notebooks, code, and data). 
<br />  
<br />  
**Let's log in!** By log in, I mean start your remote terminal session that connects you to the CRC cluster.

When you do, you should get some text in your terminal like:

![image of cluster sign-in messages](thumbnail_image.png)

**These notifications are so important!** However, they are a bit outdated.
+ The current user guide is at [crc manual](https://crc-pages.pitt.edu/user-manual/)
+ crc-interactive may be depricated; recoomend using **slurm** commands (see below)

Most importantly, **DO NOT RUN ON THE LOGIN NODE!**
What is the login node? It's where you land after log in.
You can see your location next to your username at the commandline prompt. *YourUser*@login#

We cannot work here, so we need to request a place to work.

## The 'cluster' is composed of different clusters

The parts of the CRC ecosystem are organized into clusters designed for unique usage or tasks. 
<br />  
<br />  

| Cluster Acronym  | Full form | Usage description | Our usage |
| ------------- | ------------- | ------------- | ------------- |
| mpi  | Message Passing Interface  | For tightly coupled parallel codes that use the Message Passing Interface APIs for distributing computation across multiple nodes, each with its own memory space | none |
| htc  | High Throughput Computing  | For genomics and other health sciences-related workflows that can run on a single node | Most small to moderate tasks; ChIP-seq, C&R analysis |
| smp | Shared Memory Processing | For jobs that can run on a single node where the CPU cores share a common memory space | Any high-memory tasks; DiMeLo processing |
| gpu | Graphics Processing Unit | For AI/ML applications and physics-based simulation codes that had been written to take advantage of accelerated computing on GPU cores | Guppy basecalling requires a GPU |

<br />  
Each cluster is composed of different hardware that offers different resources. Clusters also have individual regulations on how you request resources. For instance, you cannot request more than one node at a time on the htc cluster.

You can find more information about the organization of each cluster **here:**
+ [MPI](https://crc-pages.pitt.edu/user-manual/hardware_profiles/mpi/)
+ [HTC](https://crc-pages.pitt.edu/user-manual/hardware_profiles/htc/)
+ [SMP](https://crc-pages.pitt.edu/user-manual/hardware_profiles/smp/)
+ [GPU](https://crc-pages.pitt.edu/user-manual/hardware_profiles/gpu/)

**An illustration can be very helpful**
<br />  

![resource organization](hpc-schematic.jpg)
*Read more about it here [Computing basics](https://ekatsevi.github.io/statistical-computing/hpc-basics.html)*

+ <ins>Node</ins>: a single computational unit within a cluster. Each node contains one or more CPUs and memory. A cluster can consist of a few to thousands of nodes, working together to execute large-scale computational tasks.
+ <ins>CPU (Central Processing Unit)</ins>: the primary computational engine of an HPC node. It executes the instructions of a computer program and interacts with other system components. CPUs typically have multiple cores, allowing them to process several tasks simultaneously.
+ <ins>Core</ins>: an individual processing unit within a CPU. Each core can independently execute instructions, so computational parallelization on HPC clusters typically occurs at the core level.
+ <ins>Memory/RAM (Random-Access Memory)</ins>: primary storage medium that the CPU uses to store and retrieve data. Each node has its own RAM, which is shared among the cores on that node.

**Remember**
+ Clusters are organized in a resource heirarchy         Cluster > partition > node > CPU > core
+ Always refer to the cluster organization to design your resource request--your request will be denied if the requested resources cannot be given



We need to request the resources we need for the task we want to perform. 


