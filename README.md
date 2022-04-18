# ChIPLine Example
Attempting to install and run the ChIPLine Pipeline. Following the main instructions located over here: https://github.com/ay-lab/ChIPLine. There are several packages but I am mostly worried about setting up the R-environment, everything else should work fine. Several of the specialized packages that we will need are actually coming from [phantompeakqualtools](https://github.com/kundajelab/phantompeakqualtools) and are already listed below. It is very important that phantompeakqualtools instructions are followed since they provide the clearest documentation for installing things like the `spp`package.

During this installation I also realized that maybe I had changed my `~/.R/Makevars` too much so I copied over the one provided to the whole system under `/usr/lib64/R/etc/Makeconf`. 



# Attempt #1: Relying on Mamba
For R we need:
- [ ] R 3.4.3
- [ ] caTools
- [ ] snow
- [ ] snowfall
- [ ] bitops
- [ ] Rsamtools (in Bioconductor)
- [ ] spp (1.14, 1.15.x)

```
qsub -I -l walltime=200:00:00,mem=20gb
```

Create a new environment
```
mamba create -n chipline -c r r-base=3.4.3 r-essentials
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

Install clang for compiling
```
mamba install -c conda-forge/label/broken clang=14.0.0
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

# Attempt #2: Relying on Mamba and R 3.6.1
- R 3.6.1 (The ChiPLine notes actually say to use R 3.4.3 but caTools is not available for it)

- [x] R 3.6.1
- [x] caTools
- [x] snow
- [x] snowfall
- [x] bitops
- [x] Rsamtools (in Bioconductor)
- [x] spp (1.14, 1.15.x) # ended up using 1.15.3

```
qsub -I -l walltime=200:00:00,mem=20gb
```

Create a new environment
```
mamba create -n chipline -c conda-forge r-base=3.6.1 r-essentials
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
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("Rsamtools")
install.packages("./spp_1.14.tar.gz")
```

# Other notes
- May need to run an installion of the tbb package which is a dependency of Bowtie2:
```
mamba install tbb=2020.2
```

# Attempt #2b: R 3.6.1 from the shared
/share/apps/R/3.6.1/bin/R

- [x] R 3.4.3
- [x] caTools
- [x] snow
- [x] snowfall
- [x] bitops
- [x] Rsamtools (in Bioconductor)
- [x] spp (1.14, 1.15.x) # ended up using 1.15.3

Saving this just in case but skip for now
```
install.packages("devtools")
require(devtools)
devtools::install_github('hms-dbmi/spp', build_vignettes = FALSE)
```

Install the first 5 packages
```
install.packages("snow", repos="http://cran.us.r-project.org")
install.packages("snowfall", repos="http://cran.us.r-project.org")
install.packages("bitops", repos="http://cran.us.r-project.org")
install.packages("caTools", repos="http://cran.us.r-project.org")
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("Rsamtools")
```

Install spp using the remotes packages, a two step process
```
install.packages("remotes")
library(remotes)
install_version("spp", "1.15.3")
```

```
When the prompt appears type 1 + Enter
```
