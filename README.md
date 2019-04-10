# WT-Noah-MP User Guide
###### - Water tracer enabled version of Noah-MP (based on Noah-MP version 4.0)

###### - Tracer code developed by by Huancui Hu ([Hu et al. 2018, Journal of Hydrometeorology](https://journals.ametsoc.org/doi/full/10.1175/JHM-D-17-0202.1))

###### - Contact Email: huancuihu@gmail.com


#### Compile and run original Noah-MP (without tracer):
   - Follow “Readme_GLDAS” to compile the model and prepare initial and forcing data to drive the model
   - See [https://github.com/NCAR/hrldas-release/tree/master/HRLDAS](https://github.com/NCAR/hrldas-release/tree/master/HRLDAS)
   
***
### The following part will focus on running water tracer enabled version of Noah-MP (WT-Noah-MP):

#### How to compile WT-Noah-MP?
You’ll need to replace a few modules with tracer enabled versions and then recompile.

- Replace a couple of codes:
1.  In "IO_code/" directory:

```sh
cp module_NoahMP_hrldas_driver_wt.F module_NoahMP_hrldas_driver.F
```
