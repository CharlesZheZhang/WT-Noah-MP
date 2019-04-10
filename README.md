# WT-Noah-MP User Guide
###### Water tracer enabled version of Noah-MP (based on Noah-MP version 4.0)

###### Tracer code developed by by Huancui Hu ([Hu et al. 2018, Journal of Hydrometeorology](https://journals.ametsoc.org/doi/full/10.1175/JHM-D-17-0202.1))

###### Contact Email: huancuihu@gmail.com

---
### Compile and run original Noah-MP (without tracer):
   - Follow “**Readme_GLDAS**” to compile the model and prepare initial and forcing data to drive the model
   - See [https://github.com/NCAR/hrldas-release/tree/master/HRLDAS](https://github.com/NCAR/hrldas-release/tree/master/HRLDAS)

***
#### The following part will focus on running water tracer enabled version of Noah-MP (WT-Noah-MP):

## A. How to compile WT-Noah-MP?
You’ll need to **replace** a few modules with tracer enabled versions and then **recompile**.

### 1. Replace a couple of codes

- **In "IO_code/" directory:**

```sh
cp module_NoahMP_hrldas_driver_wt.F module_NoahMP_hrldas_driver.F
```

```sh
cp module_hrldas_netcdf_io_wt.F module_hrldas_netcdf_io.F
```
###### (the original codes without tracer are in *module_NoahMP_hrldas_driver_original.F* and *module_hrldas_netcdf_io_original.F*)

- **In "phys/" directory:**
```sh
cp module_sf_noahmpdrv_wt.F module_sf_noahmpdrv.F
```
```sh
cp module_sf_noahmplsm_wt.F module_sf_noahmplsm.F
```
###### (the original codes without tracer are in *module_sf_noahmpdrv_original.F* and *module_sf_noahmpdrv_original.F*)

### 2. Compile WT-Noah-MP
- **Enter directory _“xxxx/hrldas-release-master/HRLDAS”_**
- **Enter command line:**
```sh
./configure
```
- **Enter selection according to your compiler**

(I used “Linux ifort compiler serial” for single-column simulation)
- **It will create a file “user_build_options”**

In this file, you’ll probably need to change the directories for _“INCJASPER”, “NETCDFMOD” and “NETCDFLIB”_ accordingly

- **Then use command line “make” to compile the model**
```sh
make clean; make
```
- **Successful compilation should generate executable program _“hrldas.exe”_ in _“xxxx/hrldas-release-master/HRLDAS/run/”_**


## B. How to run WT-Noah-MP?
You’ll need to have the **_"namelist.hrldas"_** file in order to run the model.

- **Enter directory “xxxx/hrldas-release-master/HRLDAS/run/”**
- **An _namelist_ example is shown as “namelist.hrldas.WS10_7layer_7tracer”**
- **Adjust the time period for simulation, input/output directories accordingly**
- **Adjust the part for _“water tracer tagging configuration”_**


>a) Specify “WATER_TRACER_OPTION” and “PARTIAL_MIXING_OPTION”
>
>b) Use “track_start” and “track_end” to specify the during for precipitation tagging
>
>c) The number of sublayers (see Figure 2 in [**Hu et al. 2018**](https://journals.ametsoc.org/doi/full/10.1175/JHM-D-17-0202.1), Journal of Hydrometeorology, for reference) in each soil layer can be specified by _“tracer_sublayer(x)”_

- **Copy this modified version to be _“namelist.hrldas”_**
```sh
cp namelist.hrldas.WS10_7layer_7tracer namelist.hrldas
```
- **Run the model**
```sh
./hrldas.exe
```
###### (paralleled computation should use other commands to assign nodes)

---
Note: this version does not output tracer vars in restart file; cannot read in tracer vars from restart file
