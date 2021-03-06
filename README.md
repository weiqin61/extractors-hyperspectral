# Hyperspectral extractors

This repository contains extractors that process data originating from:
- Hyperspec INSPECTOR SWIR camera
- Hyperspec INSPECTOR VNIR camera


### Hyperspectral extractor
This extractor processes HDF files into netCDF. 

_Input_

  - Evaluation is triggered whenever a file is added to a dataset
  - Checks whether the file is a _raw file
  
_Output_

  - The dataset containing the _raw file will get a corresponding .nc netCDF file

## Scripts:
1. hyperspectral_workflow.sh

This is the main shell script:

- -c dfl_lvl  Compression level [0..9] (empty means none) (default )
- -d dbg_lvl  Debugging level (default 0)
- -h          Create indices file. This has the same root name as out_fl but with the suffix "_ind.nc"    
- -I drc_in   Input directory (empty means none) (default )
- -i in_fl    Input filename (required) (default )
- -j job_nbr  Job simultaneity for parallelism (default 6)
- -m msk_fl   location of Netcdf Soil Mask (Level 1 data) applied when creating indices file
- -n nco_opt  NCO options (empty means none) (default )
- -N ntl_out  Interleave-type of output (default bsq)
- -O drc_out  Output directory (default /home/butowskh/terraref/extractors-hyperspectral/hyperspectral)
- -o out_fl   Output-file (empty derives from Input filename) (default )
- -p par_typ  Parallelism type (default bck)
- -t typ_out  Type of netCDF output (default NC_USHORT)
- -T drc_tmp  Temporary directory (default /gpfs_scratch/arpae/imaging_spectrometer)
- -u unq_sfx  Unique suffix (prevents intermediate files from sharing names) (default .pid140080)
- -x xpt_flg  Experimental (default No)


2. CalculationWorks.py

A supporting module for EnvironmentalLoggerAnalyser.py and JsonDealer.py.
This module is in charge of all the calculation works needed in the
EnvironmentalLoggerAnalyser.py (converting the data made by environmental logger)
and JsonDealer.py (group up the supporting files for data_raw).

* EnvironmentalLoggerAnalyzer.py

This module will read data generated by Environmental Sensor and convert to netCDF file

* JsonDealer.py

This module parses JSON formatted metadata and data and header provided by LemnaTec and outputs a formatted netCDF4 file

* DataProcess.py

This module will process the data file and export a netCDF with variables 
from it and dimesions (band, x, y) from its hdr file

* terraref.nco

NCO/ncap2 script to process and calibrate TERRAREF exposure data
