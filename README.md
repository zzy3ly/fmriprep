README for Dockerfile: Neuroimaging Analysis Environment Setup
This README details the Dockerfile used for setting up a neuroimaging analysis environment. The Dockerfile is tailored for neuroimaging research and includes various tools and libraries essential in this field.

Overview
The Dockerfile starts from a base development image and installs numerous dependencies and neuroimaging tools. It covers everything from basic utilities to specific neuroimaging packages like FreeSurfer, FSL, and AFNI. The environment variables are set for each tool, ensuring seamless integration and functionality within the Docker container.

Dockerfile Breakdown
Base Image
FROM base:dev
We start with base:dev as our base image, providing a solid foundation with essential tools and libraries.

Installing Dependencies
RUN apt-get update && \
    apt install -y npm && \
    apt install -y libeigen3-dev && \
    apt-get install libqt6charts6-dev && \
    apt install -y qtbase5-dev libqt5opengl5-dev libqt5svg5-dev && \
    apt-get -y install mrtrix3 && \
    pip install itk && \
    pip install scipy pandas scikit-learn scikit-image && \
    pip install pillow pyqt5 pyvistaqt fury dipy nibabel nipype pydicom && \
    pip install darkdetect mne mne_connectivity ipywidgets ipyevents h5py && \
    pip install fmriprep
This section installs necessary packages including npm, various libraries like Eigen3, Qt, and Python packages essential for neuroimaging like MRtrix3, ITK, DIPY, and fmriprep.

Copying Required Software Packages
WORKDIR /tmp
COPY MRIPackages /tmp
MRI packages required for the environment are copied into the /tmp directory.

Setting Up Neuroimaging Tools
RUN tar -xzvf freesurfer-linux-ubuntu22_amd64-7.3.2.tar.gz -C /opt && \
    rm freesurfer-linux-ubuntu22_amd64-7.3.2.tar.gz && \
    unzip -d /opt/ workbench-linux64-v1.5.0.zip && \
    tar -xvf bids-validator-1.8.0.tar.gz -C /opt && \
    rm bids-validator-1.8.0.tar.gz && \
    python3 fslinstaller.py -V 6.0.6.2  -d /opt/fsl && \
    rm -rf /opt/fsl/src && \
    tar -xvf node-v20.11.0-linux-x64.tar.xz -C /opt
Installs and configures FreeSurfer, Workbench, BIDS Validator, FSL, and Node.js.

Setting Environment Variables
Various environment variables are set for Node.js, FreeSurfer, FSL, ANTs, DSI-Studio, and other tools.

Installation of bids-validator
WORKDIR /opt/bids-validator-1.8.0
RUN npm install -g bids-validator
Globally installs the BIDS Validator.

Installation of MCR and Setting Up FreeSurfer
WORKDIR /opt/freesurfer/bin
RUN ./fs_install_mcr R2019b
ENV FREESURFER_HOME=/opt/freesurfer
ENV PATH=/opt/freesurfer/bin:$PATH
Installs MATLAB Compiler Runtime for FreeSurfer and sets up the environment for FreeSurfer.

Additional Environment Variable Settings
Sets up environment variables for Workbench, FSL, ANTs, DSI-Studio, and AFNI.

Installing AFNI and Related Dependencies
RUN apt-get install -y --no-install-recommends \
    software-properties-common dirmngr && \
    curl -O https://cloud.r-project.org/bin/linux/ubuntu/marutter_pubkey.asc && \
    cat /tmp/marutter_pubkey.asc >> /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc && \
    add-apt-repository -y "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran40/" && \
    apt-get install -y --no-install-recommends \
    python-is-python3 && \              
    python3-matplotlib python3-numpy
RUN curl -O https://afni.nimh.nih.gov/pub/dist/bin/misc/@update.afni.binaries
RUN tcsh @update.afni.binaries -package linux_ubuntu_16_64 -do_extras -bindir /opt/afni
Installs AFNI along with necessary Python packages and additional dependencies.

Final Configuration
ENV R_LIBS="/opt/R"
RUN mkdir $R_LIBS
ENV PATH="$PATH:/opt/afni"
RUN rPkgsInstall -pkgs ALL
RUN cp /opt/afni/AFNI.afnirc ~/.afnirc && \
    suma -update_env && \
    apsearch -update_all_afni_help
Sets up the R environment, installs all R packages, and performs the final configuration for AFNI.

This Dockerfile is tailored for creating a comprehensive neuroimaging analysis environment, integrating a wide range of tools and libraries necessary for processing and analyzing neuroimaging data.
