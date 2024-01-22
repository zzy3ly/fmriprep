# Docker Image for Multi-Gene Analysis Tools

This Dockerfile is designed to build a Docker image containing various bioinformatics tools used for multi-gene analysis. The image is based on the `conda3:three` base image and includes popular tools such as **FastP**, **FastQC**, **Fqtools**, **BWA**, **AnnotSV**, **Plink**, **GCTA**, **R**, **BreakDancer**, and **GATK4** from the `bioconda` channel. Additionally, it incorporates specific versions of other tools such as **bcftools**, **ANNOVAR**, **samtools**, **ROOT**, **OpenSSL**, and **CNVnator**.

## Tools Included

The Dockerfile installs the following tools:

- **FastP**
- **FastQC**
- **Fqtools**
- **BWA**
- **AnnotSV** (version 3.3.6)
- **Plink**
- **GCTA**
- **R**
- **BreakDancer** (version 1.4.5)
- **GATK4** (version 4.1.8.1)
- **bcftools** (version 1.16)
- **ANNOVAR** (downloaded from [baishujun.com](https://www.baishujun.com/wp-content/uploads/2020/06/2020061107593651.zip))
- **samtools** (version 1.19)
- **ROOT** (version 6.22.08)
- **OpenSSL** (version 1.1.1v)
- **CNVnator** (version 0.3.2)

## Building the Image

To build the Docker image, save the provided Dockerfile, and run the following command:

```bash
docker build -t multi_gene_tools:latest .

Running the Container
Once the image is built, you can run a container based on this image using:

docker run -it multi_gene_tools:latest /bin/bash

This command opens an interactive shell within the container, allowing you to execute commands and use the installed tools.

Environmental Variables
The Dockerfile sets the following environment variables:

PATH: Adds tool directories to the system's executable search path.
ROOTSYS: Specifies the ROOT installation directory.
LD_LIBRARY_PATH: Adds library directories to the system's library search path.

Tool-Specific Configurations
bcftools: Downloads version 1.16 and sets the installation path to /opt/bcftools-1.16.
ANNOVAR: Downloads from a specific URL and extracts to /opt/ANNOVAR.
samtools: Downloads version 1.19, configures installation path to /opt/samtools-1.19/, and disables curses and lzma.
ROOT: Downloads version 6.22.08, extracts to /opt/root, and applies a modification to a specific header file.
OpenSSL: Downloads version 1.1.1v, configures installation path to /opt/openssl-1.1.1v.
CNVnator: Downloads version 0.3.2, extracts to /opt/CNVnator_v0.3.2/, creates symbolic links to samtools and ROOT, and compiles samtools.

Important Notes
Ensure Docker is installed on your system before building and running the container.
The Dockerfile assumes a Linux-based system, and certain tools may have system-specific dependencies.
The container starts with an interactive shell, allowing further customization or execution of specific tool commands.
Feel free to modify the Dockerfile or the provided commands according to your specific requirements or system constraints.
