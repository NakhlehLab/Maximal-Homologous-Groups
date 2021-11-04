# Maximal-Homologous-Groups

### **Main Function** Integrated Two-Step
```
usage: MHG.py [-h] [-g GENOME] [-b BLAST] [-db DATABASE] [-q QUERY] [-w WORD_SIZE] [-T THREAD] [-go GAPOPEN] [-ge GAPEXTEND] [-o OUTPUT] [-t THRESHOLD]

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
usage: genome_to_blast_db.py [-h] [-g GENOME] [-b BLAST] [-db DATABASE] [-q QUERY] [-w WORD_SIZE] [-T THREAD] [-go GAPOPEN] [-ge GAPEXTEND]

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
usage: MHG_partition.py [-h] [-q QUERY] [-o OUTPUT] [-t THRESHOLD]

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