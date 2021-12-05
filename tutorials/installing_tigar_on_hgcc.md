---
layout: page
permalink: /tutorials/installing-tigar-hgcc
title: Installing TIGAR on HGCC
---

<h2>Login</h2>

1. Login to HGCC.
1. Request an interactive session using 
```bash
qlogin
```
1. Do NOT load the Anaconda module at any point during installation, or before running TIGAR. The setup will fail if Anaconda is loaded. If you have loaded the Anaconda module, you will need to exit the session and log back in. 

<h2>Install Miniconda</h2>

1. Download the latest Miniconda installer for Linux from <a href="https://docs.conda.io/en/latest/miniconda.html">the conda website</a> (Note the link and filename may be different):
```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

1. Verify your installation: This step ensures that the file you downloaded is correct. The checksum output from the following code MUST match the file's SHA256 hash shown on <a href="https://docs.conda.io/en/latest/miniconda.html">the conda website</a>. 
```bash
sha256sum Miniconda3-latest-Linux-x86_64.sh
```
Identical files have the same checksum; your download should have the same checksum as the original file. If your file's checksum doesn't match the expected value, it may be corrupted. Delete it, re-download, and try again. If this still doesn't work, search online to see if other people are having the same issues with conda or contact the conda developers.

1. Install. 
```bash
# ensure the file is executable
chmod 755 Miniconda3-latest-Linux-x86_64.sh
# run the install script
bash Miniconda3-latest-Linux-x86_64.sh
```

1. Add the conda script directory to your PATH, an environment variable that tells bash where to look for programs. Adding the script directory to your PATH variable will let you run the conda from other directories. To temporarily change the current value of PATH, do the following (be sure to change `myusername` to your HGCC username):
```bash
# look at your current PATH
echo $PATH
# update your PATH variable for this session
export PATH=/home/myusername/miniconda3/bin/:$PATH
# look at your updated PATH
echo $PATH
```
The PATH variable will be reset next session, but it's useful to permanently add the conda script directory to your PATH. In order to do that, you need to edit your bash configuration file, `.bashrc.user`, located in your home directory on HGCC. Be sure to change `myusername` to your HGCC username:
```bash
# go to your home directory (in case you're not already there)
cd
# view the files in your directory
ls
# view the files in your directory, including hidden files
ls -a
# add the command used to update your PATH variable to the end of your ~/.bashrc.user file
echo 'export PATH=/home/myusername/miniconda3/bin/:$PATH' >> ~/.bashrc.user
```
The .bashrc.user configuration file stores commands you that you want to run every time you start a session; changes to this file will take effect the next time you log in (i.e., updating the `.bashrc.user` won't update the value of PATH for the current session). 
<!-- This configuration file is similar to the .bash_profile file found on OSX or other Linux computers. -->


<h2>Install the Python Environment</h2>

1. Create a Python 3.5 environment called `tigarenv` and install the Python packages required by TIGAR in it.
```bash
# create the environment tigarenv
conda create --name tigarenv python=3.5 pandas numpy scipy scikit-learn statsmodels
```
The `tigarenv` environment is now installed. 

1. (Optional). Deactivate the `tigarenv` environment. If you're done using the environment, switch back to the base environment using 
```bash
# deactivate the conda environment
conda deactivate
```

<h2>Install TIGAR</h2>

1. Go to your preferred directory for installing GitHub repositories. If you don't have one, you can create a directory
```bash
# create a new directory called github in your home directory(but dont cause an error if it already exists)
mkdir -p ~/github
```

1. Clone the TIGAR repository inside your github directory.
```bash
# go to your github directory
cd ~/github
# clone the TIGAR repository in the current directory
git clone https://github.com/yanglab-emory/TIGAR.git
```

1. Make TIGAR scripts executable (be sure to change `myusername` to your HGCC username):
```bash
# make all of the scripts ending with .sh in the tigar directory executable
TIGAR_dir="/home/myusername/github/TIGAR"
chmod 755 ${TIGAR_dir}/*.sh 
# make the DPR script executable 
chmod 755 ${TIGAR_dir}/Model_Train_Pred/DPR
```

TIGAR is now installed and ready to run. 


<h2>Running TIGAR</h2>

1. Activate the `tigarenv` Python environment
```bash
# activate the environment
conda activate tigarenv
# set the PYTHONPATH
export PYTHONPATH=${CONDA_PREFIX}/lib/python3.5/site-packages/:$PYTHONPATH
```

1. Run your job using the instructions and examples found on the <a href="https://github.com/yanglab-emory/TIGAR">TIGAR GitHub page</a>.

1. Deactivate the `tigarenv` Python environment.
```bash
conda deactivate
```


<!-- If you did not install in your home directory, check the correct install location to use instead:
```bash
pwd
``` -->













