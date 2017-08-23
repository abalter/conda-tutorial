# Hands-On with Conda

## Install miniconda sandbox
* Download installation script from https://conda.io/miniconda.html.
* You can choose to install to your Mac or a directory on styx or exacloud.
* Choose the appropriate installer for your platform.
* "Appropriate" also means Python 3x because we are in the 21st century. If you need to run a P2x package, create an environment for it.
* Run the script. For example: `bash Miniconda3-latest-MacOSX-x86_64.sh`
* When you get to this prompt: 

```
Miniconda3 will now be installed into this location:
/Users/balter/miniconda3

  - Press ENTER to confirm the location
  - Press CTRL-C to abort the installation
  - Or specify a different location below

[/Users/balter/miniconda3] >>>
```

  Enter the place where you want your sandbox installation. For example: `~/conda_test`
  
* Set your path to use conda FIRST:

        export PATH="~/conda_test/bin:$PATH"

* Hopefully your `PYTHONPATH` and other library paths won't cause problems. 

## Add Channels

```
conda config --add channels conda-forge
conda config --add channels anaconda
conda config --add channels r
conda config --add channels bioconda
```

## Install Some Packages

    conda install r r-essentials gatk picard samtools STAR bedtools bwa fastqc r-data.table bioconductor-limma bioconductor-qvalue
    
Notice the various languages these are written in:

* https://github.com/broadgsa/gatk
* https://github.com/broadinstitute/picard
* https://github.com/samtools
* https://sourceforge.net/projects/bio-bwa/
* https://www.bioinformatics.babraham.ac.uk/projects/fastqc/

## Install Something with PIP

    pip install bioepic

## See What You Have Installed 

    conda env export --name root -f test.yml
    cat test.yml
    
If you needed to reproduce it, you can use:

    conda env create -f test.yml
    
## Conda with different versions of software

### Problem: The MACS2 peak caller is written in Python 2.7 (Hey it was originally written in 2008).

Try to install the `macs2` peak caller:

    conda install macs2
    
This is what I got:

```
balter@BICB260:~$ conda install macs2
Fetching package metadata ...................
Solving package specifications: .


UnsatisfiableError: The following specifications were found to be in conflict:
  - macs2 -> python >=2.7,<3
  - python 3.5*
Use "conda info <package>" to see the dependencies for each package.
```

### Solution: 

1. Create an environment based on Python 2.7

        conda create --name macs2 python=2.7

2. Activate the environment 

        source activate macs2

3. Install macs2

        conda install macs2

4. Check

        macs2 -h
        macs2 --version

### Comment:
You can actually do the entire install in one step: `conda create --name macs2 macs2`. 
This will install macs2 and all dependencies including Python 2.7 automatically.

## To Do

- [ ] When you install an R package using `install.pacakges` in R, where does it go?  
- [ ] Do you need to clear your R path variables?  

  

