# predSS
Predictive signatures for patient survival based on gene expression data.
# =======================
predSS : Predictive Signatures for Survival analysis functions


INSTALLATION & RUNNING MANUAL
Version 1.0 (July 1 2020)
Joachim Theilhaber


INTRODUCTION :

This is a set of R-based functions for the generation of signatures
for prediction or prognosis of patient survival using covariates based
on gene expression profiling. These functions were used in data
analysis the paper : 

Construction and optimization of gene expression signatures for
prediction of survival in two-arm clinical trials Joachim Theilhaber;
Marielle Chiron; Jennifer Dreymann; Donald Bergstrom; Jack
Pollard. BMC Bioinformatics (2020)

As shown in the example below (section Examples), all of the functions
in the package have been made callable by 'driver' functions which
mimic a command-line submission and make the corresponding processing
easy to implement in an automated pipeline.


PREREQUISITES :

* Required version of R: 3.6.1 or higher.

* Required libraries: 

   survival
   glmnet
   data.table
   hwriter
   MASS
   data.table
   Hmisc
   vioplot
   limma

* Platforms : Windows 7, 10; Mac OS; linux/UNIX
              To run 'make' under Windows you will need a UNIX
              emulator such as CYGWIN.

* Total code length: 39620 lines (excluding comments).


INSTALLATION :

* Do :

   tar xvzf predSS.tar.gz 

to unpack the installation. This will create a set of directories
under the root directory 'predSS'.

Go in to directory predSS. In file 'Makefile' change the setting for variable
RBIN to reflect the local R installation (this is the only change to
be done). 

A list of available functions can be found in the file :
 
    R.functionDescriptions-version01.xlsx


EXAMPLES :

* Running examples using 'make' :

     make cleantmp     Deletes all output and temporary plot files.
     make test         Runs a gallery of tests, using many datasets as input. Total running time
                       is about 30 minutes. Shorter tests can be done by applying make to some of 
                       the sub- or subsub- targets.

* Running examples within an R session :

Within an R session, do :

       # ...........................................................................................................................
       # . Load all functions :
       # ...........................................................................................................................
       setwd("d:/my-ROOT/R-Programs/predSS");                  # Set path to wherever the local directory was unpacked.
       source("./regression/src/R/util/loadSuperPc.r");        # These load the requisite Cox regression functions.
       source("./utilities/src/R/util/loadUtilities.r");       # These load the requisite utilities functions.
       # ...........................................................................................................................
       # . Useage : for all of the driver functions, you can retrieve a description of the parameters by typing :
       # ...........................................................................................................................
       run_basic_cox_cv_with_cov_single("-use");
       # ...........................................................................................................................
       # . Generating CV results on a CRC data set :
       # . First build a command line.
       # ...........................................................................................................................
       cmd = "";
       cmd = paste(cmd, "-fx ./data/Gene-expression/BGI-CRC-clin-209-4-17-2015-quant-Log2-ZTRAN-laurentpuig-57-corrZETA-noREPs.FLAT");
       cmd = paste(cmd, "-fe ./data/Gene-expression/BGI-CRC-clin-209-4-17-2015-quant-Log2-ZTRAN-laurentpuig-57-corrZETA-noREPs.DF");
       cmd = paste(cmd, "-flagCenter yes");  
       cmd = paste(cmd, "-tTime timePFS");  
       cmd = paste(cmd, "-tStatus censPFS");  
       cmd = paste(cmd, "-tTrain NONE");  
       cmd = paste(cmd, "-tCov treatmentIttZ");  
       cmd = paste(cmd, "-methodSplit vfoldStrict");  
       cmd = paste(cmd, "-tSplit NONE");  
       cmd = paste(cmd, "-ft 0.2");  
       cmd = paste(cmd, "-ncv 20");  
       cmd = paste(cmd, "-rngSeed 789123");  
       cmd = paste(cmd, "-hRC 1");  
       cmd = paste(cmd, "-flagQlist no");  
       cmd = paste(cmd, "-fs ./data/Gene-expression/output_files/DEMO-209-Log2-ZTRAN-laurentpuig-57-corrZETA-CV-ft02.STAT");  
       cmd = paste(cmd, "-fo ./data/Gene-expression/output_files/DEMO-209-Log2-ZTRAN-laurentpuig-57-corrZETA-CV-ft02.COXCV");
       cmd = paste(cmd, "-flagPlot yes");  
       cmd = paste(cmd, "-flagPlotWrite yes");  
       cmd = paste(cmd, "-dirPlot ./data/Gene-expression/output_files/tmp");  
       cmd = paste(cmd, "-fplot ./data/Gene-expression/output_files/tmp/DEMO-209-Log2-ZTRAN-laurentpuig-57-corrZETA-CV-ft02.PLOT");  
       # ...........................................................................................................................
       # . Now submit :
       # ...........................................................................................................................
       run_basic_cox_cv_with_cov_single(cmd);
       # ...........................................................................................................................

# =============================================================================================================================
