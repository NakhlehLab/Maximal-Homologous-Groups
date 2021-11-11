# Maximal-Homologous-Groups

[![Anaconda-Server Badge](https://anaconda.org/bioconda/mhg/badges/installer/conda.svg)](https://anaconda.org/bioconda/mhg)  [![Anaconda-Server Badge](https://anaconda.org/bioconda/mhg/badges/downloads.svg)](https://anaconda.org/bioconda/mhg)

MHG stands for Maximal Homologous Group. Inputting genome nucleotide seqeunces, MHG is an annotation-free graph-based tool to merge and partition homologous groups, and outputs homologous groups for the target genome set where each group has its evolutionary history as a single tree and involves no rearrangements. The below sections introduce three sub-programs and you can find an testing example case in the latter section:
1. MHG: Start from nucleotide sequences to build blastn databases and queries. And then partition for MHGs.
2. genome-to-blast-db: Start from nucleotide sequences, only build blastn databases and queries.
3. MHG-partition: Start from Blastn queries, only partition for MHGs.

## Installation Option 1: conda install
It is highly recommended to setup a new conda environment to avoid weird stuck through conda install! Installing MHG via conda will save the time figuring out the dependencies.
```
conda create --name mhg python=3.7 
conda activate mhg
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
conda install -c bioconda mhg
```

If you encounter errors running directly ```conda install -c bioconda mhg```, try the three conda config above;

If you are stuck on "solving environment", run ```conda config --remove channels conda-forge```, and then ```conda config --add channels conda-forge``` should solve the problem.

But again, it is highly recommend to create a brand new environment. 

## Installation Option 2: git clone 
Using git clone, please install the below dependencies manually:

> [Networkx](https://networkx.org/)

> [Biopython](https://biopython.org/)

> [BEDtools](https://bedtools.readthedocs.io/en/latest/)

Also, there are required built-in python packages:

> [numpy] (https://pypi.org/project/numpy/)

> [pandas] (https://pypi.org/project/pandas/)

> [argparse] (https://pypi.org/project/argparse/)



### **Main Function** Integrated Two-Step
Please make sure to add the below two executable as two environment variables if you installed via git clone instead of conda. 

```
usage: MHG [-h] [-g GENOME] [-b BLAST] [-db DATABASE] [-q QUERY] [-w WORD_SIZE] [-T THREAD] [-go GAPOPEN] [-ge GAPEXTEND] [-o OUTPUT] [-t THRESHOLD]

Make blastn database & Build blastn queries

optional arguments:
  -h, --help            show this help message and exit
  -g GENOME, --genome GENOME
                        Genome nucleotide sequence directory (Required)
  -b BLAST, --blast BLAST
                        Blastn bin directory; try to call 'makeblastdb, blastn' straightly if no path is inputted by default(if blast folder is added as an environemnt variable
  -db DATABASE, --database DATABASE
                        Directory to store blast nucleotide databases for each sequence in genome directory. By default write to current folder 'blastn_db'
  -q QUERY, --query QUERY
                        Output folder storing all blastn queries in xml format. By defualt write to current folder 'blastn_against_bank'
  -w WORD_SIZE, --word_size WORD_SIZE
                        Blastn word size, default 28
  -T THREAD, --thread THREAD
                        Blastn thread number, default 1
  -go GAPOPEN, --gapopen GAPOPEN
                        Blastn gap open penalty, default 5
  -ge GAPEXTEND, --gapextend GAPEXTEND
                        Blastn gap extend penalty, default 2
  -o OUTPUT, --output OUTPUT
                        File containing the final partitioned MHGs, each line represents a MHG containing different blocks
  -t THRESHOLD, --threshold THRESHOLD
                        Bitscore threshold for determining true homology
```


### **BLASTn** Pairwise Alignment
```
usage: genome-to-blast-db [-h] [-g GENOME] [-b BLAST] [-db DATABASE] [-q QUERY] [-w WORD_SIZE] [-T THREAD] [-go GAPOPEN] [-ge GAPEXTEND]

Make blastn database & Build blastn queries

optional arguments:
  -h, --help            show this help message and exit
  -g GENOME, --genome GENOME
                        Genome nucleotide sequence directory (Required)
  -b BLAST, --blast BLAST
                        Blastn bin directory; try to call 'makeblastdb, blastn' straightly if no path is inputted by default(if blast folder is added as an environemnt variable
  -db DATABASE, --database DATABASE
                        Directory to store blast nucleotide databases for each sequence in genome directory. By default write to current folder 'blastn_db'
  -q QUERY, --query QUERY
                        Output folder storing all blastn queries in xml format. By defualt write to current folder 'blastn_against_bank'
  -w WORD_SIZE, --word_size WORD_SIZE
                        Blastn word size, default 28
  -T THREAD, --thread THREAD
                        Blastn thread number, default 1
  -go GAPOPEN, --gapopen GAPOPEN
                        Blastn gap open penalty, default 5
  -ge GAPEXTEND, --gapextend GAPEXTEND
                        Blastn gap extend penalty, default 2
```

### **MHG Partition** Alignment Graph Construction and Traversal
```
usage: MHG-partition [-h] [-q QUERY] [-o OUTPUT] [-t THRESHOLD]

Partition and generate modules

optional arguments:
  -h, --help            show this help message and exit
  -q QUERY, --query QUERY
                        Input folder for module partition storing all blastn queries in xml format
  -o OUTPUT, --output OUTPUT
                        File containing the final partitioned modules, each line represents a module containing different blocks
  -t THRESHOLD, --threshold THRESHOLD
                        Bitscore threshold for determining true homology
```


### Testing Case
```
MHG -g genomes/ -t 0.95
```

The command builds blastn databases and runs blastn queries, and partition for MHGs for four sample bacteria locatated in *genomes* with a bitscore threshold 0.95 (A Query with bit score above 95% of maximum bit score is considered as a true homology; a more detailed description of the threshold can be found in our paper). This example should run about 20-30 minute outputted to *mhg.txt* where each line is a MHG. This should have about 1000 MHGs. 
