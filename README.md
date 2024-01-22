Docker Image for Advanced Neuroimaging and Processing Tools
This Dockerfile is designed to build a Docker image equipped with a comprehensive suite of neuroimaging and processing tools. The image is based on the base:dev base image and includes a wide array of specialized software and libraries for advanced neuroimaging analysis. This includes tools like MRtrix3, FreeSurfer, FSL, ANTs, DSI-Studio, and more, along with various Python libraries and Node.js.

Tools and Libraries Included
The Dockerfile installs the following tools and libraries:

NPM (Node Package Manager)
Libraries for Eigen3, Qt5, and Qt6
MRtrix3: A software package for diffusion MRI analysis
ITK (Insight Segmentation and Registration Toolkit)
Python libraries: scipy, pandas, scikit-learn, scikit-image, pillow, pyqt5, pyvistaqt, fury, dipy, nibabel, nipype, pydicom, darkdetect, mne, mne_connectivity, ipywidgets, ipyevents, h5py, fmriprep
FreeSurfer: A software package for analyzing and visualizing human brain MRI images
Connectome Workbench
BIDS Validator
Node.js
BIDS Validator (Node.js version)
MATLAB Runtime (MCR) for FreeSurfer
ANTs (Advanced Normalization Tools)
DSI-Studio: A diffusion MRI analysis and visualization tool
AFNI (Analysis of Functional NeuroImages)
R and related packages for AFNI
Building the Image
To build the Docker image, save the provided Dockerfile and run the following command:
docker build -t neuroimaging_tools:latest .
Running the Container
Once the image is built, you can run a container based on this image using:
docker run -it neuroimaging_tools:latest /bin/bash
This command opens an interactive shell within the container, allowing you to execute commands and use the installed tools.

Environmental Variables
The Dockerfile sets several environment variables to configure paths for the installed tools, including:

PATH: Updated to include paths for Node.js, FreeSurfer, Workbench, FSL, ANTs, and DSI-Studio.
FREESURFER_HOME, FSLDIR, FSLOUTPUTTYPE, FSLMULTIFILEQUIT, FSLTCLSH, FSLWISH, FSLGECUDAQ, FSL_LOAD_NIFTI_EXTENSIONS, FSL_SKIP_GLOBAL: Specific to FreeSurfer and FSL configurations.
ANTSPATH, DSISTUDIOPATH: Paths for ANTs and DSI-Studio.
R_LIBS: Directory for R libraries used by AFNI.
Tool-Specific Configurations and Installations
FreeSurfer, FSL, and ANTs are installed and configured with specific environment variables.
Node.js and BIDS Validator (Node.js version) are installed and their paths are added to the system's executable search path.
AFNI is installed along with R and its packages, and configured with the necessary environment variables.
Important Notes
Ensure Docker is installed on your system before building and running the container.
The Dockerfile is tailored for a Linux-based system and may have dependencies specific to this environment.
After starting the container, you can further customize it or run specific commands related to the installed neuroimaging tools.
Modifications to the Dockerfile or commands can be made to suit specific requirements or system constraints.





