# mike
## Requirements

C++ version: C++11

R Language version: 3.2.2 or higher

python version: 3.6 or higher

**Attention: if you use C++17 maybe reports errors.**

## Installation
```bash
git clone https://github.com/Argonum-Clever2/mike.git
cd mike/src
make
Rscript install.r
```

## Tutorial
### the first step
You need to install KMC in advance, and then run command below. The file will be processed into a kmer file. Or you can input the kmer file directly, just skip the step.
 
```python
# help
python kmc.py
# run
python kmc.py -f file1 file2 file3 file4 file5 file6 -d dirpath
```
### the second step 
#### kmer file
the format of a kmer file should like below, it is a string of kmer and the frequency.

AAAAAAAAAAAAAAAAAAAAA   255

AAAAAAAAAAAAAAAAAAAAC   255

AAAAAAAAAAAAAAAAAAAAG   255

AAAAAAAAAAAAAAAAAAAAT   255

AAAAAAAAAAAAAAAAAAACA   255

AAAAAAAAAAAAAAAAAAACC   255

AAAAAAAAAAAAAAAAAAACG   255

...   ...

#### filelist
filelist means a list of kmer file:

absolute_path/kmer_file_1

absolute_path/kmer_file_2

absolute_path/kmer_file_3

...   ...


#### SKETCH
sketch the genome skims, and the sketch file is in destination_path.
```bash

./mike sketch -t 10 -l filelist -d destination_path

```
#### sketch_filelist
the **sketch__filelist** is the a list of file obtained in the previous step.

the format of sketch_filelist like this:

0       1 

1       35   

2       4  

3       4   

4       10      

...   ...


#### the Jaccard coefficient 
compute the jaccard coefficient for pairwire
```bash

./mike compute -l filelist_1 -L filelist_2 -d destination_path

```

#### the evolutionary distance

compute the evolutionary distance
```bash

./mike dist -l sketch_filelist_1 -L sketch_filelist_2 -d destination_path

```

#### construction the phylogenetic tree

using the evulutionary distance to construct the phylogenetic tree without branch length
```bash
Rscript draw.r -f dist.txt -o dist.nwk
```
