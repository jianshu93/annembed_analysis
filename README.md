# Scripts for reproducing [annembed](https://crates.io/crates/annembed) paper
## All scripts are in the scripts folder to directly produce figures in the paper
###
This is a colloboration between [Jianshu Zhao](https://github.com/jianshu93) and [Jean Pierre-Both](https://github.com/jean-pierreBoth) (algorithm part). In the scripts folder, you can see the R scripts used to reproduce the main figures in the paper. 

### Simple case for install
```
### Linux
wget https://github.com/jianshu93/annembed/releases/download/v0.1.0/annembed_Linux_x86-64_v0.1.0.tar.gz
tar -xzvf annembed_Linux_x86-64_v0.1.0.tar.gz
chmod a+x ./annembed
./annembed -h

### Macos
wget https://github.com/jianshu93/annembed/releases/download/v0.1.0/annembed_Darwin_universal_v0.1.0.tar.gz
tar -xzvf annembed_Darwin_universal_v0.1.0.tar.gz
chmod a+x ./annembed
### check install MacOS, you may need to change the system setup to allow external binary to run by type the following first and use your admin password
sudo spctl --master-disable
./annembed -h

### or if you have conda installed on linux (recommended)
conda install -c bioconda annembed

### or you can have Homebrew on MacOS installed first then (recommended):
brew tap jianshu93/annembed
brew install annembed
annembed -h

```

### Usage
Annembed can be run like this (see the example input format): 
```
### prepare data
git clone https://github.com/jianshu93/annembed_analysis
cd annembed_analysis
annembed --csv ./example/C_elegan_embedded_try.csv embed --scale 0.65 --nbsample 10 --stepg 2.0 --layer 0
```
By default, annembed will use all available computer cores/threads for nearly all steps. Annembed library can be found here: https://github.com/jean-pierreBoth/annembed. Annembed can also be used as a library, as shown in the Ann section of [GSearch](https://github.com/jean-pierreBoth/gsearch)

### Output explanation
you will find a 2 column output embedded.csv by default, which are the embedded dimensions 1 and 2 respectively. Sample order are preserved and can be combined with sample metadata. Each run can be different because initialization is random and edge sampling is also random. But the visualization results will not be changed.

## Embedding genome database via [GSearch](https://github.com/jean-pierreBoth/gsearch) (install GSearch first)
```
### download pre-built bacterial genome HNSW graph database, check GSearch page ann section on how to do it
wget http://enve-omics.ce.gatech.edu/data/public_gsearch/GTDBv207_v2023.tar.gz
tar xzvf ./GTDBv207_v2023.tar.gz
cd ./GTDB/prot
tar xzvf k7_s12000_n128_ef1600.prob.tar.gz
gsearch ann -b ./k7_s12000_n128_ef1600_gsearch --stats --embed

```

The output of this step can be visualized, for example for the GTDB v207 we have the following plot. A new paper for the library and also this subcommand is in preparation.

![Alt!](https://github.com/jean-pierreBoth/gsearch/blob/master/GSearch-annembed-GTDBv207.jpg?raw=true)

### Reference
Zhao et.al., 2023, Annembed: Graph-based Approximate Nearest Neighbor Embedding Provides Fast and Efficient Dimension Reduction with Applications in Large-scale Biological Data [bioRxiv]()