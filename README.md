<img src="nanoTRF.png" width="550" >

# NanoTRF: software tool to *de novo* search high-copy tandem repeats in Oxford Nanopore Technologies (ONT) plant DNA sequencing data


## <a name="getting"></a>Getting Started
### <a name="building"></a>Building  nanoTRF from  source files

Download the [latest release](https://github.com/Kirovez/nanoTRF/releases):
```
wget https:/https://github.com/Kirovez/nanoTRF/releases/download/v1.0.0/nanoTRF-v1.0.0.tar.gz
tar -zxvf nanoTRF-v1.0.0.tar.gz && cd TideHunter-v1.0.0
```
Install via conda (recommended):
 ```
 conda env create -f nanoTRF.yml
 conda activate nanoTRF
 (nanoTRF) python3 ./nanoTRF.py -r test.fasta -pTH  -cu ./bin/canu -o./test/
 ```
or install all programs specified below and run data with special flags to specify the programs path:
- blastn and makeblastdb programs
- TideHunter programm
- Canu programm
- python >= v3.6 python packages to be installed: biopython, networkx (run command: pip install matplotlib biopython networkx)
- java
 ```
 conda env create -f nanoTRF.yml
 conda activate nanoTRF
 (nanoTRF) python3 ./nanoTRF.py -r test.fasta -pTH  -cu ./bin/canu -o./test/
  ```
 

## Table of Contents

- [Introduction](#introduction)
- [Installation](#install)
  - [Installing nanoTRF via conda](#conda)
  - [Building nanoTRF from source files](#building)
- [Getting Started](#getting) 
- [Usage](#usage)
- [Commands and options](#cmd)
- [Input](#input_output)
- [Output](#output)
- [Authors](#authors)
- [License](#license)

## <a name="introduction"></a>Introduction

NanoTRF is software tool to *de novo* search high-copy tandem repeats which is designed for raw long-read sequnces. It works with Oxford Nanopore Technologies (ONT) and Pacific Biosciences (PacBio) sequencing data.

## <a name="install"></a>Installation

### <a name="conda"></a>Installing nanoTRF via conda
On Linux/Unix, nanoTRF can be installed via creating an environment from an environment.yml file:
 ```
 conda env create -f nanoTRF.yml
 ```
For running nanoTRF, please activate the conda environment:
 ```
 conda activate nanoTRF
 ```
 Your environment is ready to be used!
 
### <a name="conda"></a>Pre-built binary executable file for Linux/Unix

If you meet any issue with creating environment, please try the pre-built binary file:

```
wget https:/https://github.com/Kirovez/nanoTRF/releases/download/v1.0.0/nanoTRF-v1.0.0.tar.gz
tar -zxvf nanoTRF-v1.0.0.tar.gz && cd TideHunter-v1.0.0
```
Before you start, you need to make sure that all program and packages specified below is already installed on your computer. For running nanoTRF  you will need to specify the programs path through special flags:

- blastn and makeblastdb programs. The paths to these programs can be set via **-b** and **-mb** flags, respectively
- TideHunter programm. It is recommended to download the [latest release of TideHunter](https://github.com/yangao07/TideHunter/releases).The paths to these programs can be set via **-pTH** flags
- Canu programm. The latest release [can be download here](http://github.com/marbl/canu/releases). The paths to these programs can be set via **-cu** flags
- java
- python >= v3.6
- 
- python packages to be installed: biopython, networkx To install these packages run the following command
```
 pip install matplotlib biopython networkx python-louvain
```
or
```
pip3 install matplotlib biopython networkx python-louvain
```
Important note! If you have community python module installed you need to delete it because it interferes with python-louvain module used by nanoTRF. Use this command to delete community module:
```
pip3 uninstall community
```


## <a name="usage"></a>Usage

To generate consensus sequences in FASTA format file (with usage default optional arguments):
```
python3 ./nanoTRF.py -r test.fasta -pTH  -cu ./bin/canu -o./test/
```
To generate consensus sequences in FASTA format file, change number of theads that will be used and remove 
all unnecessary files and directories (with usage TideHunter files) :
```
python3 ./nanoTRF.py -r test.fasta --cu ./bin/canu -o ./test/ -th 30 -d -T TH.tab TH.out.fasta
```
## <a name="cmd"></a>Command and options
```

Options:
  General options:
      -h --help               show this help message and exit
 

  Input:
    -r --reads          STR      path to FastQ or Fasta file (required argument!!!)
    -T --run_th         STR      path to output files of the TideHunter (if previously TideHunter was running by user): 
                                 table file with consensus sequnces and fasta file with uniq tandem repeats
  Scoring parameters for partial order alignment:
    -w --wordsize       INT      word size for wordfinder algorithm (length of best perfect match) [22]
    -w_f --wordsize_f   INT      word size for wordfinder algorithm (length of best perfect match) in 
                                 the Reclusting module [15]
    -ev --evalue        INT      expectation value (E) threshold for saving hits [2]

  Clustering parameters:
    -m --max_abundancy  STR      the proportion of amount lengths all tandem repeats in one cluster to length all the reads [0.0001]
    -mOVe --min_Overlap STR      the number of overlapping nucleotides between repeats in one cluster [10]
    -ca --perc_abund    STR      minimum value of the TR cluster abundancy. ***Default = 0.009***

  Path to programm for running nanoTRF:
    -pTH --path_TH      STR      path to the location of TideHunter [TideHinter]
    -cu --canu          STR      path to the location of Canu (required argument!!!It's missing in the conda)
    -trf --TRF_run      STR      path to the location [trf]
    -b --blast          STR      path to blastn executabled [blastn]
    -mb --makedb        STR      path to makeblastdb executable [makeblastdb]

  Output:
    -o --out_directory  STR      path to work directory for output files where will be saved **(required argument!!!)
    -lg --log_filepath  STR      path to file which list analysis parameters, modules and files,contains messages generated 
                                 in the various stages of the work [loging.log]
    -nano --nano_trf    STR      fasta file with the TRs consensus sequences [nanoTRF.fasta]
    -tab --nano_tab     STR      table file with the TRs abundancy [TR_info.tab]

  Сomputational resources:
    -th, --threads      STR      number of threads for running blast, canu. [4]

  Additional option:
    -d --dir_cleanup    STR      remove unncessary large files and directories from working directory [False]
    
    
-h, --help  - show this help message and exit

```
## <a name="input_output"></a>Input
NanoTRF works with FASTA and FASTQ formats.

## <a name="output"></a>Output
### <a name="output"></a>Tabular file
NanoTRF generates output in tabular format:
| №   | Column name | Description | 
|:---:|   :---      | ---        |
|  1  | Cluster     | Name and cluster number |
|  2  | TRs length  | Length of the TRs consensus sequence |
|  3  | Abundance   |  |



### <a name="output"></a>Fasta file

NanoTRF generates TRs consensus sequences in FASTA format which contents information about TRs. The sequence descriptions have the following format:
```
>clustname monomer_length cluster_abund

clustname          cluster number (for example: clust0)
monomer_length     length of the TRs sequnce
cluster_abund      cluster abundancy
```
## <a name="authors"></a>Authors
**Ilya Kirov** [kirovez@gmail.com ](kirovez@gmail.com )

**Elizaveta Kolganova** [liza.colg@gmail.com](liza.colg@gmail.com)

## <a name="license"></a>License
This project is licensed under the **MIT** License



