Version: 2021.03 release, on Aug 24, 2021. Downloaded on Oct 20,2022 

# port AM4 on stellar
(based on /tigress/wenchang/AM4_github_20190805/AM4/README.tigercpu.md)

## step 1: download the source code
cd /projects/GEOCLIM/username
git clone --recursive https://github.com/NOAA-GFDL/AM4.git

## step 2: modify the template file $(exec)/templates/intel.mk (make a backup if necessary)
cd ./AM4
cd ./exec/templates
# change intel.mk as following (former to latter):

181c181
< LIBS += -lhdf5 -lhdf5_fortran -lhdf5_hl -lhdf5_hl_fortran
---
> LIBS += -lhdf5 -lhdf5_fortran -lhdf5_hl -lhdf5hl_fortran

## step 3: prepare the environment file `set_env.sh` under $(exec):
cd ..
(use vim to write a file 'set_env.sh')

#!/usr/bin/env bash
module purge
module load intel/19.1
module load intel-mpi/intel/2019.7
module load netcdf/intel-19.1/hdf5-1.10.6/intel-mpi/4.7.4
module load hdf5/intel-19.1/intel-mpi/1.10.6


## step 4: build the model under $(exec):
source set_env.sh
make