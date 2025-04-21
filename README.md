# **Bioinformatics with Pitt's Center for Research Computing (CRC) cluster**
*YNA lab training series, pt 1*



## What is the cluster?
![Image depicting accessing the cluster from your computer.](https://crc-pages.pitt.edu/user-manual/_assets/img/getting-started/getting-started-map.png)
*Image from CRC user manual*

The 'cluster' refers to the $$\textnormal{\color{darkorange}CRC ecosystem}$$ that contains the total footprint of the CRC infrastructure, including high performance computing clusters, data storage systems, networking equipment, and software. For us, we can simply imagine it as a giant, stronger, faster computer. 

Why are we using it? A typical laptop or personal computer does not have enough storage space or $$\textnormal{\color{darkorange}resources}$$ (Memory, Processing power) to analyse many sequencing files.
+ CUT&RUN ~ 3 Gb per experiment
+ DiMeLo-seq ~ 20 Gb per experiment  
\
The storage footprint of sequencing files can double or triple during analysis.

We conenct to the CRC cluster through our $$\textnormal{\color{darkorange}Client}$$, which is the software we are using on our personal computer to interact with the CRC cluster. Our interactions with the cluster pass through an $$\textnormal{\color{darkorange}Access Portal}$$, or a remote server that take the information we submit from our client and passes it on to the CRC cluster. \
 \
$$\textnormal{\color{darkorange}Access portals}$$ are typically remote servers, which refers to a computer system that is accessed over a $$\textnormal{\color{darkorange}network}$$ , like the internet, allowing users to store, manage, and access data and applications from anywhere with an internet connection, rather than being physically located in the same place as the user.

For us, our **client(s)** are Pitt's $$\textnormal{\color{darkorange}VPN}$$ software, which gives us access to Pitt's secure private network, and our $$\textnormal{\color{darkorange}terminal emulator software}$$ (MobaXterm or Termius), which allows us to establish a connection to the CRC. 

What is a $$\textnormal{\color{darkorange}VPN}$$? It's a **Virtual Private Network**. Essentailly it is a security blanket being wrapped around your internet connection to prevent others from seeing what you are doing and to provide increased security. In our case, Pitt's VPN forced us to prove who we are (your pitt username and password), it authenticated us (it agreed we are that person), and then it allowed us access to the PITT network from our personal computer. This keeps non-PITT people out of Pitt's network and they cannot access the cluster. 


Why is it called a $$\textnormal{\color{darkorange}terminal emulator}$$? Take yourself way back in your imagination to when computers were huge and took up an entire room. The box that controlled the computer was called the terminal. Here, the terminal emulator is serving the same function for the CRC cluster, but instead of being connected to the giant computer (cluster), it's giving commands to the giant computer over the internet. 

Our $$\textnormal{\color{darkorange}access portal}$$ refers to how we are interacting with the cluster. We will primarily interact through the 'login node' pictured above. CRC also provides user access to viz (in-browser Linux Desktop environment on the CRCD system), OnDemand (requesting resources for interactive visual software, etc) and JupyterHub (web-based interactive development environment for notebooks, code, and data). 
<br />  

## Logging in to the cluster
**Let's log in!** By log in, I mean start your remote terminal session that connects you to the CRC cluster.

If you have already installed PITT's VPN and a terminal emulator and set them up with the guidance [here](https://crc-pages.pitt.edu/user-manual/getting-started/terminal/), you will be able to log in with your PITT username and password. 

When you do, you should get some text in your terminal like:

<div align="center">
 <img src="https://github.com/mmahlke/Training/blob/main/thumbnail_image.png" alt="image of cluster sign-in messages" style="width:50%; height:50%;">
</div>

**These notifications are so important!** However, they are a bit outdated.
+ The current user guide is at [crc manual](https://crc-pages.pitt.edu/user-manual/)
+ crc-interactive may be depricated; recommend using $$\textnormal{\color{darkorange}SLURM}$$ commands (see below)

Most importantly, **DO NOT RUN ON THE LOGIN NODE!** \
What is the login node? It's where you land after log in. It's like the waiting room. \
You can see your location next to your username at the command line prompt. 
<br />  
```[user123@login1 ~]$  ```
## Using the command line on the cluster
Now that our terminal is connected to the CRC cluster, if we want to issue commands we have to speak in the computer's language so it can understand us. First, let's get an idea of how the CRC's logistic layers are arranged. 

<div align="center">
 <img src="https://github.com/mmahlke/Training/blob/main/shell_layers.png" alt="computing layers" style="width:50%; height:50%;">
</div>

*Source:https://mindmajix.com/shell-scripting-tutorial*

The cluster's $$\textnormal{\color{darkorange}kernel}$$ is run by [Linux](https://en.wikipedia.org/wiki/Linux), as opposed to an operating system like MacOS or Windows. The kernel is he primary interface between the computer's hardware and the software processes running on it.

The cluster is also 'wrapped' by a command-line interface (CLI) program that allows users to interact with the kernel by typing commands. This $$\textnormal{\color{darkorange}'shell'}$$ wrapping the kernel is called [BASH](https://en.wikipedia.org/wiki/Bash_(Unix_shell)) (or Bourne Again Shell). 

The language(s) we speak to the computer in are either **Linux** or **Bash**. You will find a lot of murky language discussing Bash and Linux. In fact, it's easy (and common) to confuse Linux and Bash commands. And really there are only small differenes in when we use them. Technically, BASH commands are a subset of Linux commands focused on shell scripting, whereas Linux commands encompass a larger set of tools. Bash is primarily a user interface for communicating with Linux, though Linux commands exist outside of Bash and can also be executed on the command line. 

There are many websites with cheat sheets for basic Bash and Linux commands. I like [this](https://www.geeksforgeeks.org/linux-commands-cheat-sheet/) and [this](https://cheatography.com/davechild/cheat-sheets/linux-command-line/) but there are so many amazing resources out there that you can find. If you have time, take a look [here](https://github.com/jlevy/the-art-of-command-line).  

Don't ignore $$\textnormal{\color{darkorange}built-in help options}$$ that come with utilities in the command line. 
For example, if using `tar`, try:
```
$ man tar

$ info tar

$ tar --help
```
The best resource is your search engine. Want to do something but do not know how? Ask Google or ask ChatGPT.
<br />

Ok, so we are using our **terminal emulator** software to speak **BASH** to the **Linux** kernel governing CRC's cluster hardware. 

Let's run some basic commands in the login node that do not require any resources.

+ Use `sinfo` to return the status of all clusters.

+ Use `crc-usage yarbely` to check on our storage allocation and what users are associated with it. 

+ Use `du -sh <directory_path>` to see how much space a directory is taking up on our storage allocation.

+ Or use `df -h <directory_path>` to see how much space we used and how much is available in our allocation.


Other than small commands, we cannot work on the login node so we need to request a place to work.

## The 'cluster' is composed of different clusters

The parts of the $$\textnormal{\color{darkorange}CRC ecosystem}$$ are organized into clusters designed for unique usage or tasks. 
<br />  
<br />  

| Cluster Acronym  | Full form | Usage description | Our usage |
| ------------- | ------------- | ------------- | ------------- |
| mpi  | Message Passing Interface  | For tightly coupled parallel codes that use the Message Passing Interface APIs for distributing computation across multiple nodes, each with its own memory space | none |
| htc  | High Throughput Computing  | For genomics and other health sciences-related workflows that can run on a single node | Most small to moderate tasks; ChIP-seq, C&R analysis |
| smp | Shared Memory Processing | For jobs that can run on a single node where the CPU cores share a common memory space | Any high-memory tasks; DiMeLo processing |
| gpu | Graphics Processing Unit | For AI/ML applications and physics-based simulation codes that had been written to take advantage of accelerated computing on GPU cores | Guppy basecalling requires a GPU |

<br />  
But what are nodes, cores, CPUs, etc?
<br />  
<br />  

**An illustration can be very helpful**
<br />  

<div align="center">
  <img src="https://github.com/mmahlke/Training/blob/main/hpc-schematic.jpg" alt="resource organization" style="width:75%; height:75%;">
</div>

*Read more about it here [Computing basics](https://ekatsevi.github.io/statistical-computing/hpc-basics.html)*

+ <ins>Node</ins>: a single computational unit within a cluster. Each node contains one or more CPUs and memory. A cluster can consist of a few to thousands of nodes, working together to execute large-scale computational tasks.
+ <ins>CPU (Central Processing Unit)</ins>: the primary computational engine of an HPC node. It executes the instructions of a computer program and interacts with other system components. CPUs typically have multiple cores, allowing them to process several tasks simultaneously.
+ <ins>Core</ins>: an individual processing unit within a CPU. Each core can independently execute instructions, so computational parallelization on HPC clusters typically occurs at the core level.
+ <ins>Memory/RAM (Random-Access Memory)</ins>: primary storage medium that the CPU uses to store and retrieve data. Each node has its own RAM, which is shared among the cores on that node.

Each cluster is composed of different hardware that offers different resources. Clusters also have individual regulations on how you request resources. For instance, you cannot request more than one node at a time on the htc cluster.

You can find more information about the organization of each cluster **here:**
+ [MPI](https://crc-pages.pitt.edu/user-manual/hardware_profiles/mpi/)
+ [HTC](https://crc-pages.pitt.edu/user-manual/hardware_profiles/htc/)
+ [SMP](https://crc-pages.pitt.edu/user-manual/hardware_profiles/smp/)
+ [GPU](https://crc-pages.pitt.edu/user-manual/hardware_profiles/gpu/)

  
$$\textnormal{\color{darkorange}Remember:}$$
+ Clusters are organized in a resource heirarchy
  + Cluster > partition > node > CPU > core
+ Always refer to the cluster organization to design your resource request--your request will be denied if the requested resources cannot be given
+ Request the right resources for the task you want to perform


## SLURM resource manager

**SLURM (Simple Linux Utility for Resource Management) resource manager** is a system for requesting resources from the cluster. Once you request resources, they are assigned to you as a $$\textnormal{\color{darkorange}'job'}$$ that comes with a Job ID. You can request two different types of $$\textnormal{\color{darkorange}jobs}$$ with slurm:
+ **Interactive jobs** will run directly in your terminal emulator and you can interact with them using the command line prompt
+ **Batch jobs** are submitted directly to the cluster and run in the background--you do not see them being executed but you can specify diffeernt types of output to understand how they ran or are running

The four main commands we use for slurm are:
+ `srun` to submit an interactive job
+ `sbatch` to submit a batch job from a .txt file
+ `squeue` to check the status of all jobs you have submitted that are running
+ `scancel` to cancel a running job
<br />   

When requesting a job with slurm, there are many [options](https://slurm.schedmd.com/documentation.html). However, there are a few things we **MUST** include for the request to be completed:
+ `-t HH:MM:SS ` how long we would like our resources to be available to us in hours, minutes, seconds format
+ `-M or --cluster <htc, smp, mpi, gpu> ` the cluster we are requesting resources from
+ `--partition <partition name>` to specify the partition needed on the cluster
+ `--pty bash` to provide a bash pseudoterminal in **interactive mode**

Recommended options:
+ `--cpus-per-task` to specify how many CPUs to use for your task, this helps split tasks across multiple CPUs and complete them more efficiently
+ For **batch scripts**:
  + `--job-name=<name>` to specify a easy to read name for your job that you can see in job manager with `squeue`
  + `--error=<path/for/error/messages.txt>` and `--output=<path/to/save/terminal/output.txt.` to give you some readout on what happened/is happening in batch jobs running in the background

[Here](https://slurm.schedmd.com/pdfs/summary.pdf) is a cheat sheet to the basic slurm commands.

## Requesting an interactive job
**Let's request an interactive job and leave the login node**

You can request an interactive session with `srun`. Here's and example requesting an $$\textnormal{\color{darkorange}interactive job}$$ on the htc cluster for 1 hour:

```srun -t 01:00:00 --cluster htc --partition htc --cpus-per-task=8 --pty bash```

You will recieve notification of your resource request and notification when it is granted. Resource requests can take longer to fill if you request a greater share of the resources. This is true for interactive and batch jobs. If resources are currently unavailable, you will be placed in a $$\textnormal{\color{darkorange}queue}$$. 
Once resources are granted, you will see in your terminal that you are no longer in the login node and are now working in a node on the htc cluster. \
 \
 `[user123@htc-657-n3 ~]$` 

 If we enter `squeue -u <username> --cluster htc`, we will see our currently running job that we requested resources for on the htc cluster listed in the $$\textnormal{\color{darkorange}queue}$$.

 **Now that we have a workspace, let's grab some files to practice with.**

 There are $$\textnormal{\color{darkorange}4 directories}$$ (folders, file paths) that you will work with on the cluster:
 + `/ihome/yarbely/<your_username>` is your personal home folder and scratch space
   + you can store small files here like models, custom scripts or whatever you please
   + when you build a virtual environment, it will be installed here
   + you can also custom install packages/utilities here   
 + `/ix1/yarbely/<your_username>` is your main data working area (your benchtop)
   + perform all data analyses in this large space
   + our storage allocation is shared by the entire lab    
 + `/ix1/yarbely/Data` is our operational space for storing new sequencing data
   + **NEVER** modify files in this folder
   + Copy them to your data benchtop before analyzing 
 + `/bgfs/yarbely/Data` is our 'defunct' space for storaing sequencing data
   + **NEVER** modify files in this folder
   + Copy them to your data benchtop before analyzing
   + We will never recieve more storage space here; if we remove things no longer used to a different storage space, we can add new things here

First, let's check our current location in the directory of all the files:\
```$ pwd  ```\
   \
Your current directory is often called your working directory (ie. the directory you are currently working in). `pwd` stands for "print working directory", so identify and return our current directory.

Let's change our directory to the space we want to work in:\
```$ cd /ix1/yarbely/<your_username>  ```

Now create a file that we can put all of our training stuff into:\
```$ mkdir -p /ix1/yarbely/<your_username>/training/CR_PDNC4  ``` 

The `-p` option here instructs Linux to make the directories recursively--meaning all required directories and subdirectories will be created. If we try this command without `-p` it will fail because it will try to create directory `CR_PDNC4` in directory `training` which doesn't exist yet.

Let's copy some files into our training directory so we can investigate them:\
```$ cp -r /bgfs/yarbely/Data/CUT_RUN/Pool_4/01.RawData/YNA_4_1/. /ix1/yarbely/<your_username>/training/CR_PDNC4  ```
+ YNA_4_1 is a PD-NC4 control sample
+ copy command syntax is `cp <source> <destination>`
+ /.../YNA_4_1/.    the '.' at the end means the source is all files and folders inside of /YNA_4_1 directory
+ cp by default does not copy directories unless you specify the -r (recursive) option
 
Notice the $$\textnormal{\color{darkorange}file extension}$$ at the end of the file name. It ends with ".fq.gz". This indicates that the normal extension for the files is .fastq but it has been compressed with `gzip` utility. \ 
  \
**Let's unzip them:**
```
cd /ix1/yarbely/<your_username>/training/CR_PDNC4 
gunzip *.gz 

```
Here, using the $$\textnormal{\color{darkorange}wildcard symbol (*)}$$ means perform this operation on all files in the current directory with any name and ending with `.gz` .

Now we have our unpacked files. Let's **re-name** them so we don't have to continue using the really long sequencing file name. We can rename them simply by using the SSH file connection panel. Let's call them **PDNC4_1.fq** and **PDNC4_2.fq** for simplicity. 

Most sequencing data starts as .fasta or .fastq (the more current version of .fasta) format. Let's investigate the structure of a .fastq file.

```
head -n 20 PDNC4_1.fq
```
`head` is a Linux/BASH command that lets us see the beginning of a file. By default, it returns the first 5 lines of a file. Here, we specify the number of lines to display with ` -n 20 `. \
`tail` command will show you the last -n lines of a file.

A FASTQ file has four line-separated fields per sequence:

+ Field 1 begins with a '@' character and is followed by a sequence identifier and an optional description (like a FASTA title line).
+ Field 2 is the raw sequence letters.
+ Field 3 begins with a '+' character and is optionally followed by the same sequence identifier (and any description) again.
+ Field 4 encodes the quality values for the sequence in Field 2, and must contain the same number of symbols as letters in the sequence.

It's silly to go through the reads and try to interpret what the quality values are. But we can use a command line utility (aka a **module**) to do that for us. 

## Running modules on the cluster
$$\textnormal{\color{darkorange}Modules}$$ are like software that run without a visual user interface. Instead, you will load them in Linux (starting them up, essentially), and then speak to them with their own unique sets of commands. 

Each module is a tool created by a person or group to complete a specific task or set of tasks. As such, most modules have their own guides on how to use them, which can be intricate. 

To start off, lets use `lmod` the module management utility to investigate modules on the cluster. 
```
module avail
module spider fastqc

module spider samtools
```
Module names are listed as "name/version#". Some modules will be available in several different versions. Sometimes it matters what version you use! So always track what version of a module you have used to process your data. 

Some modules have special instructions on how to load them, like samtools requires you to load module gcc/8.2.0 before loading samtools itself. Before you use a module for the first time, it's helpful to use `module spider <module_name/with_version>` to check if the module has any special requirements. `module spider <module_name>` without a version# will return all versions of that module that are available on the cluster. 

**Let's load fastqc** to perform a simple check on the .fastq files we have. 
We can also make a directory for our output to be placed into. \

```
module load fastqc/0.11.9
mkdir ./fastqc
```
` ./ ` proceeding the file name `fastqc` is a shorthand for 'current directory'. So we are making the new file called 'fastqc' in our current directory.

Let's check to see the new directory is there in our SSH files window. 

To give a command to the fastqc module, we need to use the right language that fastqc will understand. 
We can find out more about the language by typing `fastqc --help`.

Let's tell fastqc to run an analysis on one of our fastq files. The syntax we use is:
```
fastqc -o ./fastqc PDNC4_1.fq 
```
+ where -o is the output location 
+ and PDNC4_1.fq is the file to use
 
Fastqc should output a report file into the /fastqc directory for each fastq file of reads. Let's download those files and open them in our browser.

We should see something like this:
<div align="center">
  <img src="https://github.com/mmahlke/Training/blob/main/fastqc.png" alt="fastqc output" style="width:75%; height:75%;">
</div>

<br />   

Let's look at a module we will use A LOT, $$\textnormal{\color{darkorange}samtools}$$. 

```
module load gcc/8.2.0
module load samtools/1.14
samtools --help
```

$$\textnormal{\color{darkorange}Samtools}$$ has a lot of utilities that are extremely useful for processing data once it has been aligned to an assembly. \
It also has an excellent online manual you can find [here](https://www.htslib.org/doc/samtools.html).

To create an $$\textnormal{\color{darkorange}aligned sequencing file}$$, we need to take our raw reads (.fastq files) and align them to an $$\textnormal{\color{darkorange}assembly}$$. 

First, we need to download the assembly files. We can get assembly files from two places:
+ [NLM-NCBI](https://www.ncbi.nlm.nih.gov/datasets/genome/)  
+ [UCSC](https://genome.ucsc.edu/cgi-bin/hgGateway)

NCBI and UCSC assemblies contain the same information but the $$\textnormal{\color{darkorange}chromosome names are formatted diffently}$$. This is important to be aware of for later steps. 

Let's look at how we find the files we want in each location. Always read the $$\textnormal{\color{darkorange}README.txt}$$ to help you get the correct file.

Let's download the NCBI version. One thing you will might not immediately notice is that $$\textnormal{\color{darkorange}NCBI's current human assembly (GRCh38.p14)}$$ has incorporated all previously missing sequences into it from the T2T assembly. You can download the T2T assembly or you can download the human assembly with complete centromere and repetitive sequences. 

We will get the complete human assembly GRC38.p14 today. 

We can use `wget` command to download large files directly from links. 

```
pwd
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/001/405/GCF_000001405.40_GRCh38.p14/GCF_000001405.40_GRCh38.p14_genomic.fna.gz
```
Now we have an assembly and we have raw sequencing .fastq files. It's time to align them! But we don't want to do that in an interactive session--it will take some time for all the commands to complete and if we lose our internet connection, the commands will be terminated. We should submit this task as a $$\textnormal{\color{darkorange}batch job}$$. 

## Submitting batch jobs on the cluster

Submitting a $$\textnormal{\color{darkorange}batch job}$$ is equivalent to sending a list of instructions to the cluster without being able to check between steps. Sometimes this approach is called 'submitting a batch script'. 

You've probably heard the term $$\textnormal{\color{darkorange}script}$$ a lot. What does that even mean? It's exactly what it sounds like. A play has a script that tells the actors what to say, when to say, how to say, where to stand, how loud to be, etc, etc. A $$\textnormal{\color{darkorange}script}$$ is just a set of directions you supply to the cluster. 

Batch scripts are just text files and you can build them in any $$\textnormal{\color{darkorange}text editor}$$. Open whatever text editor your computer already comes equipped with. 

I like [notepad++](https://notepad-plus-plus.org/) because I like to have extra features!

To start a $$\textnormal{\color{darkorange}script}$$, we need to tell Linux what command line interface (CLI) we want to use to interpret the rest of the script. Ours is $$\textnormal{\color{darkorange}BASH}$$. The lines at the beginning of the script are called the $$\textnormal{\color{darkorange}bash shebang}$$ and starts with the characters #!. For bash scripts, it typically looks like this: `#!/bin/bash` or `#!/usr/bin/env bash`.

We also want to specify the $$\textnormal{\color{darkorange}resources and specifications}$$ that should be used for this job in the subsequent lines. For those lines, we do not need to include '!', but we will start the lines with '#' (hashtag) and follow with command `SBATCH` to specify that these are instructions to SLURM. 

In general, across many computing languages used to write scripts, lines that start with **'#'** are $$\textnormal{\color{darkorange}'read'}$$ but not $$\textnormal{\color{darkorange}'executed'}$$. Lines starting with '#' can be explicit instructions to the operating system or they can be comments for the reader/writer. Either way, Linux will interpret '#' lines are non-commands or non-executables. 

Let's start our file like this:
```
#!/bin/bash
#
#SBATCH --job-name=PDNC4_practice
#SBATCH --cluster=htc
#SBATCH --partition=htc
#SBATCH --time=24:00:00
#SBATCH --cpus-per-task=16
#SBATCH --verbose
#SBATCH --error=/ix1/yarbely/<your_user>/training/CR_PDNC4/job.%J.err
#SBATCH --output=/ix1/yarbely/<your_user>/training/CR_PDNC4/job.%J.out

```
Here, we are requesting resources for a job named "PDNC4_practice" for 24 hours on the htc cluster which has only one partition, the htc partition. We have requested 16 cpus per task. We have requested verbose output, which means any possible output to the terminal from our commands will be recorded. And we have specified files for the output and error messages to be placed into. 

Now we should tell Linux what $$\textnormal{\color{darkorange}modules}$$ we need to load to complete the tasks in this script. For this script, we will build an index for our assembly file, trim our raw reads, and align them to the assembly. To do that, we need:
```
module load cutadapt/2.10
module load gcc/8.2.0
module load bowtie2/2.4.1
```
So let's add that to the file. 

Let's also tell Linux where we want to perform this work.
```
cd /ix1/yarbely/<your_user>/training/CR_PDNC4/
```

Now we can add our commands. 

First, we will trim the reads with [CutAdapt](https://cutadapt.readthedocs.io/en/stable/) to remove any remaining adapter sequences that can interfere with alignment to the reference assembly. 
```
cutadapt \
	-m 20 \
-a AGATCGGAAGAGCACACGTCTGAACTCCAGTCA \
-A AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGT \
-o PDNC4_1.trimmed.fq -p PDNC4_2.trimmed.fq \
PDNC4_1.fq PDNC4_2.fq
```
Here, 
+ -m specifies the minimum fragment length. Anything below 20 bp will be trashed. You can change as you like.
+ -a is the forward adapter trimming sequence
+ -A is the reverse adapter trimming sequence
 + You can find both of these sequences in the documentation for the NEB Next lib prep kit. You should change this if using a different kit with different adaptor sequences.
+ -o and -p are the out files for the forward and reverse paired reads
+ the final line is the two .fastq files we are starting with

Next, we align the trimmed reads. [Bowtie2](https://bowtie-bio.sourceforge.net/bowtie2/index.shtml) is the aligning tool we will use for our CUT&RUN data. Before we can align with Bowtie2, we need to build an index for our assembly to help bowtie2 perform its job more efficiently. 

```
bowtie2-build ./GCF_000001405.40_GRCh38.p14_genomic.fna.gz h38.p14
```
Here,
+ ./GCF_000001405.40_GRCh38.p14_genomic.fna.gz is the path to the file we want to index
+ h38.p14 is the 'nickname' we want to use for the index

Now we are ready to align. Add an alignment command for Bowtie2 to the script:
```
bowtie2 \
	--end-to-end --very-sensitive --no-mixed --no-discordant -I 10 -X 700 --dovetail -p 8 \
	-x /ix1/yarbely/<your_user>/training/CR_PDNC4/h38.p14 \
	-1 PDNC4_1.trimmed.fq \
	-2 PDNC4_2.trimmed.fq \
	-S PDNC4_test.sam
```
Here, 
+ --end-to-end, --very-sensitive, --no-mixed, and --no-discordant are options that specify alignment with no mismatch to the genome assembly from both reads in a pair
+ -I 10 and -X 700 set the range of inter-mates distances
+ --dovetail means if the mates "dovetail", or if one mate alignment extends past the beginning of the other such that the wrong mate begins upstream, consider that to be concordant
 + these settings are recommended for CUT&RUN
+ -p 8 is specifying to split this process into 8 threads (to go faster)
+ -x is the location of the assembly and index with the last entry being the index 'nickname'
+ -1 and -2 are our paired raw read files
+ -S is our ouput of a .sam file

So in total, our file should look like this:

```
#!/bin/bash
#
#SBATCH --job-name=PDNC4_practice
#SBATCH --cluster=htc
#SBATCH --partition=htc
#SBATCH --time=24:00:00
#SBATCH --cpus-per-task=16
#SBATCH --verbose
#SBATCH --error=/ix1/yarbely/<your_user>/training/CR_PDNC4/job.%J.err
#SBATCH --output=/ix1/yarbely/<your_user>/training/CR_PDNC4/job.%J.out

module load cutadapt/2.10
module load gcc/8.2.0
module load bowtie2/2.4.1

cd /ix1/yarbely/<your_user>/training/CR_PDNC4

cutadapt \
	-m 20 \
-a AGATCGGAAGAGCACACGTCTGAACTCCAGTCA \
-A AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGT \
-o PDNC4_1.trimmed.fq -p PDNC4_2.trimmed.fq \
PDNC4_1.fq PDNC4_2.fq

bowtie2-build ./GCF_000001405.40_GRCh38.p14_genomic.fna.gz h38.p14

bowtie2 \
	--end-to-end --very-sensitive --no-mixed --no-discordant -I 10 -X 700 --dovetail -p 8 \
	-x /ix1/yarbely/<your_user>/training/CR_PDNC4/h38.p14 \
	-1 PDNC4_1.trimmed.fq \
	-2 PDNC4_2.trimmed.fq \
	-S PDNC4_test.sam
```
Now, we need to save the file. You can save it as 'PDNC4_alignment_test.txt' or 'PDNC4_alignment_test.bash'. 
Let's upload it to our current directory using our SSH files window.

Now we can submit this script to the cluster and let it work. 

```
[user@login-1]$ sbatch /ix1/yarbely/<your_user>/training/CR_PDNC4/PDNC4_alignment_test.txt
```
Where the command `sbatch` is followed by the full path to the file. Because this script will run in the background, we can submit it with `sbatch` from the login node or from an interactive session. 

Lastly, let's check that the script is running.
```
squeue -u <username> --cluster htc
```

In the next session, we will check on the file, perform more analysis steps, and finally see our data!










