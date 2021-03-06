# MAESPA

| Model Information ||
| -- | -- |
| Home Page |http://maespa.github.io/ |
| Source Code | http://maespa.github.io/download.html|
| License |  |
| Authors |Belinda Medlyn and Remko Duursma |
| PEcAn Integration |Tony Gardella, Martim DeKauwe, Remki Duursma |

## Introduction



## PEcAn configuration file additions

## Model specific input files



## Model configuration files

MODEL is configured using 3 files which are placed in the run folder, as well as a symbolic link to the met file.

* **file1** : template for this file is located at models/MODEL/inst/file1 and is not modified.  
* **file2** : template for this file is located at models/MODEL/inst/file2 and is not modified.  
* **file3** : template for this file is in models/MODEL/inst/file3 or it is specified in the \<model\> section as \<template\>. The values in this template are replaced by those computed in the earlier stages of PEcAN.

## Installation notes

Installing the  MAESPA model requires cloning the MAESPA Bitbucket Repository, executing the makefile, and ensuring that the Maeswarp R package is correctly installed.

To clone and compile the model, execute this code at the command line
```
git clone https://bitbucket.org/remkoduursma/maespa.git

cd maespa

make clean

make
```

```maespa.out``` is your executable. Example input files can be found in the inputfiles directory. Executing measpa.out from within one of the example directories will produce output.

MAESPA developers have also developed a wrapper package called ```Maeswrap```. The usual R package installation method ```install.packages``` may present issues with downloading an unpacking a dependency package called ```rgl```. Here are a couple of solutions:

Solution 1

### From the Command Line
sudo apt-get install r-cran-rgl

then from within R

install.packages("Maeswrap")

Solution 2

### From the Command line 
sudo apt-get install libglu1-mesa-dev

then from within R

install.packages("Maeswrap")


``` 

This section contains notes on how to compile the model. The notes for the VM might work on other machines or configurations as well.

### VM
