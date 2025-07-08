---
layout: post
title: "Interpolating CESM CAM initial condition data"
date: 2025-07-08
description: Interpolating CESM CAM initial data from one resolution to anothe
share: true
tags:
 - CESM
---

Using FORTRAN interpic_new tool 
## 1. Compiling interpic
Go to directory ~/CESM/cesm2.1.5/components/cam/tools/
Change the following part and 
```powershell
 14 ifeq ($(strip $(LIB_NETCDF)),)
 15   #LIB_NETCDF := /usr/local/lib
 16   LIB_NETCDF := $(NETCDF)/lib
 17 endif
 18 ifeq ($(strip $(INC_NETCDF)),)
 19   #INC_NETCDF := /usr/local/include
 20   INC_NETCDF := $(NETCDF)/include
 21 endif

 .....

 83 ifeq ($(UNAMES),Linux)
 84
 85 # g95
 86 #FC = g95
 87 #FFLAGS =  -c -I$(INC_NETCDF) -g -ftrace=full
 88
 89 # pgf90
 90 #FC = pgf90
 91 #FFLAGS =  -c -I$(INC_NETCDF) -g -Ktrap=fp -Mrecursive -Mbounds
 92
 93 # lf95
 94 #FC = lf95
 95 #FFLAGS =  -c -I$(INC_NETCDF) -g --chk a,e,s,u --pca --trace --trap
 96
 97 # ifort
 98 FC = ifort
 99 FFLAGS =  -c -I$(INC_NETCDF) -g -check all -fpe0 -traceback -ftz -convert big_endian -fp-model precise
 100 LDFLAGS = -L$(LIB_NETCDF) -lnetcdff -lnetcdf
 101 #LDFLAGS = -L$(LIB_NETCDF) -lnetcdf
 102 endif
```

## 2. Interpolation
```powershell
interpic -t template.nc inputfile.nc outputfile.nc
```

For example, interpolate CAM intial condition data from f19 grid to fv02 grid:
```powershell
#!/bin/bash
  dirn="~/b.e13.Bi1850C5.f19_g16.6ka.ghg_orb.control_to_fv02"
  cd ~/CESM/CESM_tools/interpic_new/
  ./interpic -t $dirn/f.e13.Fi1850C5.fv02.0ka.intann.sst.02.cam.h0.0010-12.nc  $dirn/b.e13.Bi1850C5.f19_g16.6ka.ghg_orb.control.cam.i.0061-01-01-00000.nc  $dirn/b.e13.Bi1850C5.f19_g16_to_fv02.6ka.ghg_orb.control.cam.i.0061-01-01-00000.nc
  # or
  ./interpic -o $dirn/f.e13.Fi1850C5.fv02.0ka.intann.sst.02.cam.r.0011-01-01-00000.nc -i $dirn/b.e13.Bi1850C5.f19_g16_to_fv02.6ka.ghg_orb.control.cam.r.0061-01-01-00000.nc
```

**Reference**:
(https://bb.cgd.ucar.edu/cesm/threads/interpolating-input-data-from-waccm-to-cam-chem.6987/).

Updated: 07/08/2025