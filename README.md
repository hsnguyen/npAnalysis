
#Real-time analysis of Oxford Nanopore MinION sequencing


This directory contains information for setting up real-time analysis 
of Oxford Nanopore sequencing data, as described in the under-review 
manuscript:

Real-time strain typing and analysis of antibiotic resistance potential using 
Nanopore MinION sequencing

Minh Duc Cao, Devika Ganesamoorthy, Alysha G. Elliott, Huihui Zhang, Matthew 
A. Cooper and Lachlan Coin


##Software installation

The streamline agorithms and auxiliary programs for setting up the pipeline 
are provided in japsa package (https://github.com/mdcao/japsa). In addition, the 
following free-software dependencies are required:

 1. Java >=1.7
 2. bwa >=7.10 (0.7.10-r858-dirty recommended)
 3. R with rJava and MultinomialCI installed
 4. kalign2 (http://msa.sbc.su.se/cgi-bin/msa.cgi)
 5. HDF5 (https://hdfgroup.org/HDF5/release/obtain5.html)
 -- optional, needed for translating native fast5 files to fastq

###Quick installation guide

```
git clone https://github.com/mdcao/japsa
cd japsa
make install \
   [INSTALL_DIR=~/.usr/local \]
   [MXMEM=7000m \]
   [SERVER=true \]
   [JLP=/usr/lib/jni:/usr/lib/R/site-library/rJava/jri]
```
 
This will install japsa according the directives:

* *INSTALL_DIR*: specifies the directory to install japsa, e.g, ~/.usr/local. Make sure
 you have write privilege to this folder. Also add INSTALL_DIR/bin (e.g., )
 to your PATH envirenment e.g., 
```
export PATH=~/.usr/local/bin:$PATH
```
* *MXMEM*: specifies the default memory allocated to the java virtual machine
* *SERVER*: specifies whether to launch the java virtual machine in server mode
* *JLP*: points to where HDF libraries and JRI are installed e.g,
 /usr/local/lib:/usr/lib/R/site-library/rJava/jri. The path to HDF is only needed for
 creating the pipelines to analyse directly from fast5 files or simultaneously
 from the MinION sequencing

For more detailed information for installing japsa, please refer to  Japsa installation guide on
http://japsa.readthedocs.org/en/latest/install.html

##Databases and data

Each of the analyses requires a pre-processed database. We make avaibale these databases as follow.

###Bacterial species database

We make available the database of all bacterial genomes obtained from NCBI genbank, 
with the addition of two K. quasipnuemoniae strains (see the manuscript). Download
the database (~2.8GB), and make an bwa index of the database as follows.
```
wget https://swift.rc.nectar.org.au:8888/v1/AUTH_15574c7fb24c44b3b34069185efba190/npAnalysis/SpeciesTyping.tar.gz
tar zxvf SpeciesTyping.tar.gz
cd SpeciesTyping/Bacteria/
gunzip genomeDB.fasta.gz
bwa index genomeDB.fasta.gz
```
Note that it might take a while to build the bwa index for this 9G-base database.

###Strain typing with MLST
The database for MLST typing for three species,  K. pnuemoniae, E. coli and
S. aureus are make avaibale. Download (208KB) and unzip them:
```
wget https://swift.rc.nectar.org.au:8888/v1/AUTH_15574c7fb24c44b3b34069185efba190/npAnalysis/MLST.tar.gz
tar zxvf MLST.tar.gz
```

###Strain typing with gene presence and absence
The database for gene presence and absence strain typing for K. pnuemoniae, E. coli and
S. aureus can be obtained as follows:
```
wget https://swift.rc.nectar.org.au:8888/v1/AUTH_15574c7fb24c44b3b34069185efba190/npAnalysis/StrainTyping.tar.gz
tar zxvf ResGene.tar.gz
```

###Resistance gene identification
```
wget https://swift.rc.nectar.org.au:8888/v1/AUTH_15574c7fb24c44b3b34069185efba190/npAnalysis/ResGene.tar.gz
tar zxvf ResGene.tar.gz
```

##Data

##Putting together

##Contact

Please contact Minh Duc Cao (minhduc.cao@gmail.com) for further information.


I. Obtaining data

To run the analyses, download and unzip the .gz files, i.e.:
$ wget http://genomicsresearch.org/public/researcher/npAnalysis/japsa-v1.5-5b.tar.gz && tar zxvf japsa-v1.5-5b.tar.gz
$ wget http://genomicsresearch.org/public/researcher/npAnalysis/FastqData.tar.gz && tar zxvf FastqData.tar.gz
$ wget http://genomicsresearch.org/public/researcher/npAnalysis/SpeciesTyping.tar.gz && tar zxvf SpeciesTyping.tar.gz
$ wget http://genomicsresearch.org/public/researcher/npAnalysis/MLST.tar.gz && tar zxvf MLST.tar.gz
$ wget http://genomicsresearch.org/public/researcher/npAnalysis/StrainTyping.tar.gz && tar zxvf StrainTyping.tar.gz
$ wget http://genomicsresearch.org/public/researcher/npAnalysis/ResistantGenes.tar.gz && tar zxvf ResistantGenes.tar.gz

Raw data (fast5 format) of the three strains can be obtained from European Nucleotide Archive with Study Accession Number ERP010377

III. Data

Nanopore data in fastq format are kept in FastqData.

Raw data (fast5 format) can be obtained from Sequence Read Archive, Study Accession
Number ERP010377


IV. Running analyses

The scripts, together of associated files of the analyses are in the following directories:

 1. SpeciesTyping/: species typing

 2. MLST/: Multi-locus strain typing

 3. StrainTyping/: Strain typing with gene presence/absence

 4. ResistantGenes/: Identification of antibiotic resistance gene identification

