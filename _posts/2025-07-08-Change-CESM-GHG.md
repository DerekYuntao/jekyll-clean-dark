---
layout: post
title: "Change greenhouse gases concentration in CESM simulatoins"
date: 2025-07-08
description: How to change greenhouse gases concentration in CESM AGCM and coupled simulatoins
share: true
tags:
 - CESM
---

## 1. Change GHG concentration in a coupled CESM run
If one only tend to change CO2 concentration for the whole climate system in a coupled CESM1 simulation, simply do the following change:
```powershell
./xmlchange CCSM_CO2_PPMV=264.4   #value to be propagated to POP and CLM
```

<span style="color:red;">**Note, however, that for a coupled run in CESM1, setting the user_nl_atm namelist in the following way will have no effect !!!</span>
````powershell
 cat >! user_nl_atm << EOF
 scenario_ghg = 'FIXED'
 co2vmr = 264.4e-6
 ch4vmr = 597e-9
 n2ovmr = 262e-9
 f11vmr = 0.0
 f12vmr = 0.0
 EOF
````

Alternatively, one should do this way to change other GHG concentration:
Ater creating the case, first change the CO2 concentration as *./xmlchange CCSM_CO2_PPMV=264.4*, then go to case directory: {casename}/Buildconf
Open file cam.buildnml.csh, and find the line stating "set co2vmr = "co2vmr=${CCSM_CO2_PPMV}e-6""
Then add the following lines after that (for the 6ka case):
```powershell
 set co2vmr = "co2vmr=${CCSM_CO2_PPMV}e-6"
 set ch4vmr = "ch4vmr=597e-9"
 set n2ovmr = "n2ovmr=262e-9"
 set f11vmr = "f11vmr=0.0"
```

Then continue building the model. Before sumibiting the case, make sure that associated values in *atm_in* have been successfully changed as follows:
```powershell
  &chem_surfvals_nl
  ch4vmr     = 597e-9
  co2vmr     = 264.4e-6
  f11vmr     = 0.0
  f12vmr     = 0.0
  flbc_list      = ' '
  n2ovmr     = 262e-9
```

## 2. Change GHG concentration in an AGCM run
If one only tend to change GHG concentration for the atmosphere-only (and land) component in a AGCM run, simply do the following change in *atm_in* will work:
````powershell
 cat >! user_nl_atm << EOF
 scenario_ghg = 'FIXED'
 co2vmr = 264.4e-6
 ch4vmr = 597e-9
 n2ovmr = 262e-9
 f11vmr = 0.0
 f12vmr = 0.0
 EOF
````
Also, make sure that associated values in *atm_in* have been successfully changed before submiting the case!

Updated: 07/08/2025