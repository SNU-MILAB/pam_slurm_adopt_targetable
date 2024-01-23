# pam_slurm_adopt_targetable
[pam_slurm_adopt](https://slurm.schedmd.com/pam_slurm_adopt.html) slurm plugin modified to enable specifying target slurm job

## Pre-requisites
For the plugin to work, home directory must be synced (e.g. via NFS) between slurm login node and compute nodes.

## How to install it
```bash
cp pam_slurm_adopt.c ${SLURM_BUILD_DIR}/contribs/pam_slurm_adopt/pam_slurm_adopt.c
cd ${SLURM_BUILD_DIR}/contribs/pam_slurm_adopt/
make
sudo make install
sudo ldconfig
```

## How to use it
Before ssh'ing into target host with multiple jobs, **create a plain text file named `.SSH_TARGET_SLURM_JOB_ID` containing target slurm job id in your home directory.**

## How it works

If a host has multiple jobs running, the module checks if `$HOME/.SSH_TARGET_SLURM_JOB_ID` file exists. If it does, it reads the file contents and adopts ssh into the job that has the matching job id.

After reading, the `.SSH_TARGET_SLURM_JOB_ID` file is always removed, for both successful and unsuccessful ssh connections so that you must create the file again next time.

## DISCLAIMER

This code has not been extensively tested and may have potential bugs and vulnerabilities. Use at your own discretion. 
