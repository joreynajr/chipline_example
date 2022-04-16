# chipline_example
Attempting to install and run the ChIPLine Pipeline. Following the main instructions located over here: https://github.com/ay-lab/ChIPLine. There are several packages but I am mostly worried about setting up the R-environment, everything else should work fine. Several of the specialized packages that we will need are actually coming from [phantompeakqualtools](https://github.com/kundajelab/phantompeakqualtools) and are already listed below. It is very important that phantompeakqualtools instructions are followed since they provide the clearest documentation for installing things like the `spp`package.

For R we need:
- [ ] R 3.4.3
- [ ] spp (1.14, 1.15.x)
- [ ] caTools
- [ ] snow
- [ ] snowfall
- [ ] bitops
- [ ] Rsamtools (in Bioconductor)

# Attempt #1 
- R 3.4.3

```
qsub -I -l walltime=200:00:00,mem=20gb
```

Create a new environment
```
mamba create -n chipline -c r r-base==3.4.3 r-essentials
```

Activate the chipline 
```
mamba activate chipline
```

Clone the phantompeakqualtools repository
```
git clone https://github.com/kundajelab/phantompeakqualtools
```

Navigate to the phantompeakqualtools directory
```
cd phantompeakqualtools
```

Start R session
```
R
```

Install R packages (as instructed by phantompeakqualtools
```
install.packages("snow", repos="http://cran.us.r-project.org")
install.packages("snowfall", repos="http://cran.us.r-project.org")
install.packages("bitops", repos="http://cran.us.r-project.org")
install.packages("caTools", repos="http://cran.us.r-project.org")
source("http://bioconductor.org/biocLite.R")
biocLite("Rsamtools",suppressUpdates=TRUE)
install.packages("./spp_1.14.tar.gz")
```
