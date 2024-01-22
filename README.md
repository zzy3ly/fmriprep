# Docker Image for fmriprep
This Dockerfile builds a Docker image containing a comprehensive set of neuroimaging and processing tools, perfect for advanced neuroimaging analysis. It is based on the base:dev image and includes tools like MRtrix3, FreeSurfer, FSL, ANTs, DSI-Studio, and more, along with Python libraries and Node.js.

## Tools and Libraries Included
The Dockerfile installs a diverse range of tools and libraries for neuroimaging:

- **NPM (Node Package Manager)**
- **NPM Libraries: Eigen3, Qt5, and Qt6**
- **MRtrix3**
- **ITK (Insight Segmentation and Registration Toolkit)**
- **Python libraries: scipy, pandas, scikit-learn, scikit-image, pillow, pyqt5, pyvistaqt, fury, dipy, nibabel, nipype, pydicom, darkdetect, mne, mne_connectivity, ipywidgets, ipyevents, h5py, fmriprep**
- **FreeSurfer**
- **Connectome Workbench**
- **BIDS Validator**
- **Node.js**
- **BIDS Validator (Node.js version)**
- **MATLAB Runtime (MCR) for FreeSurfer**
- **ANTs (Advanced Normalization Tools)**
- **DSI-Studio**
- **AFNI (Analysis of Functional NeuroImages)**
- **R and related packages for AFNI**

## Building the Image
To build the image, run:
docker build -t neuroimaging_tools:latest .
## Running the Container
To run the container:
docker run -it neuroimaging_tools:latest /bin/bash

## Environmental Variables
The Dockerfile sets environment variables for tools:

- **PATH: Includes Node.js, FreeSurfer, Workbench, FSL, ANTs, DSI-Studio**
- **FREESURFER_HOME, FSLDIR, FSLOUTPUTTYPE, FSLMULTIFILEQUIT, FSLTCLSH, FSLWISH, FSLGECUDAQ, FSL_LOAD_NIFTI_EXTENSIONS, FSL_SKIP_GLOBAL**
- **ANTSPATH, DSISTUDIOPATH**
- **R_LIBS**
  
## Tool-Specific Configurations
FreeSurfer, FSL, ANTs: Installed with environment variables
Node.js and BIDS Validator: Path included in PATH
AFNI: Installed with R and packages

## Notes
Ensure Docker is installed before building/running the container.
The Dockerfile is designed for Linux-based systems.
After starting the container, you can customize it or run specific neuroimaging tool commands.
Modify the Dockerfile or commands as needed.
