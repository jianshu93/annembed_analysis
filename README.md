[![install with bioconda](https://img.shields.io/badge/install%20with-bioconda-brightgreen.svg?style=flat)](https://bioconda.github.io/recipes/annembed/README.html)
![](https://anaconda.org/bioconda/annembed/badges/license.svg)
![](https://anaconda.org/bioconda/annembed/badges/version.svg)
![](https://anaconda.org/bioconda/annembed/badges/latest_release_relative_date.svg)
![](https://anaconda.org/bioconda/annembed/badges/platforms.svg)
[![install with conda](https://anaconda.org/bioconda/annembed/badges/downloads.svg)](https://anaconda.org/bioconda/annembed)

[![Latest Version](https://img.shields.io/crates/v/gsearch?style=for-the-badge&color=mediumpurple&logo=rust)](https://crates.io/crates/annembed)
[![docs.rs](https://img.shields.io/docsrs/annembed?style=for-the-badge&logo=docs.rs&color=mediumseagreen)](https://docs.rs/annembed/latest/annembed/)

<div align="center">
  <img width="50%" src ="Annembed_logo.jpg">
</div>

# Scripts for reproducing [annembed](https://doi.org/10.1093/nargab/lqae172) paper
## All scripts are in the scripts folder to directly produce figures in the paper
###
This is a colloboration between [Jianshu Zhao](https://github.com/jianshu93) and [Jean Pierre-Both](https://github.com/jean-pierreBoth) (algorithm part). In the scripts folder, you can see the R scripts used to reproduce the main figures in the paper. We have a GitLab mirror clone [here](https://gitlab.com/Jianshu_Zhao/annembed) and Gitee clone [here](https://gitee.com/jianshuzhao/annembed) (log in first) just in case Github service is not freely available in some region. 

If you find annembed useful, please cite the following paper:
```
@article{zhao2024approximate,
  title={Approximate nearest neighbor graph provides fast and efficient embedding with applications for large-scale biological data},
  author={Zhao, Jianshu and Pierre Both, Jean and Konstantinidis, Konstantinos T},
  journal={NAR Genomics and Bioinformatics},
  volume={6},
  number={4},
  pages={lqae172},
  year={2024},
  publisher={Oxford University Press}
}
```


### Simple case for stable install

```bash
conda install -c bioconda -c conda-forge annembed


### or if you have an old version miniconda3/bioconda3, use the most version number here: https://bioconda.github.io/recipes/annembed/README.html#package-package%20&#x27;annembed&#x27;
conda install -c bioconda -c conda-forge annembed=0.2.4
```


```
### Linux
wget https://github.com/jianshu93/annembed/releases/download/v0.2.4/annembed_Linux_x86-64_v0.2.4.zip
unzip annembed_Linux_x86-64_v0.2.4.zip
chmod a+x ./annembed
chmod a+x ./dmapembed
./annembed -h
./dmapembed -h
### Macos
wget https://github.com/jianshu93/annembed/releases/download/v0.2.4/annembed_Darwin_universal_v0.2.4.tar.gz
tar -xzvf ./annembed_Darwin_universal_v0.2.4.tar.gz
cd annembed
chmod a+x ./annembed
chmod a+x ./dmapembed
### check install MacOS, you may need to change the system setup to allow external binary to run by type the following first and use your admin password
sudo spctl --master-disable
./annembed -h
./dmapembed -h

### or you can have Homebrew on MacOS installed first and then (recommended):
brew update
brew tap jianshu93/annembed
brew install annembed
annembed -h

```
## Usage
```bash
$ annembed -h
 ************** initializing logger *****************

Non-linear Dimension Reduction/Embedding via Approximate Nearest Neighbor Graph, HNSW Initialization

Usage: annembed-new [OPTIONS] --csv <csvfile> [COMMAND]

Commands:
  hnsw  Build HNSW graph
  help  Print this message or the help of the given subcommand(s)

Options:
      --csv <csvfile>        Expecting a csv file
  -o, --out <outfile>        Output file name
  -d, --delim <delim>        Delimiter can be ' ', ','
      --batch <batch>        Number of batches to run [default: 20]
      --stepg <grap_step>    Number of gradient descent steps
      --nbsample <nbsample>  Number of edge sampling [default: 10]
  -l, --layer <hierarchy>    A layer num [default: 0]
      --scale <scale>        Spatial scale factor [default: 1.0]
  -d, --dim <dimension>      Dimension of embedding [default: 2]
  -q, --quality <quality>    Sampling fraction, should <= 1.
  -h, --help                 Print help

$ annembed hnsw -h
************** initializing logger *****************

Build HNSW graph

Usage: annembed --csv <csvfile> hnsw [OPTIONS] --dist <dist> --nbconn <nbconn> --ef <ef> --knbn <knbn>

Options:
  -d, --dist <dist>                    Distance type is required, must be one of   "DistL1" , "DistL2", "DistCosine" and "DistJeyffreys"  
      --nbconn <nbconn>                Maximum number of build connections allowed (M in HNSW)
      --ef <ef>                        Build factor ef_construct in HNSW
      --scale_modify_f <scale_modify>  Hierarchy scale modification factor in HNSW/HubNSW or FlatNav, must be in [0.2,1] [default: 1.0]
      --knbn <knbn>                    Number of k-nearest neighbours to be retrieved for embedding
  -h, --help                           Print help


$ dmapembed -h
Non-linear Dimension Reduction/Embedding via Approximate Nearest Neighbor Graph, Diffusion Map Initialization

Usage: dmapembed [OPTIONS] --csv <csvfile> [COMMAND]

Commands:
  hnsw  Build HNSW graph
  help  Print this message or the help of the given subcommand(s)

Options:
      --csv <csvfile>      expecting a csv file
  -o, --out <outfile>      expecting output file name
  -d, --delim <delim>      delimiter can be ' ', ','
      --alfa <alfa>        modulate laplacian with drift according to density [default: 1.0]
      --beta <beta>        value shoud be between -1. and 0. [default: 0.0]
      --time <time>        diffusion time, usually between 0. ad 5. [default: 5.0]
  -l, --layer <hierarchy>  expecting a layer num [default: 0]
  -d, --dim <dimension>    dimension of embedding [default: 2]
  -h, --help               Print help
  -V, --version            Print version


$ dmapembed hnsw -h
initializing default logger from environment ...
Build HNSW graph

Usage: dmapembed --csv <csvfile> hnsw [OPTIONS] --dist <dist> --nbconn <nbconn> --knbn <knbn> --ef <ef>

Options:
  -d, --dist <dist>                    distance is required   "DistL1" , "DistL2", "DistCosine", "DistJeyffreys"  
      --nbconn <nbconn>                number of neighbours by layer
      --scale_modify_f <scale_modify>  Hierarchy scale modification factor in HNSW/HubNSW or FlatNav, must be in [0.2,1] [default: 1.0]
      --knbn <knbn>                    number of neighbours to use
      --ef <ef>                        search factor
  -h, --help                           Print help
```


### Usage using real-world data
Annembed can be run like this (see the example input format): 
```
### prepare data
git clone https://github.com/jianshu93/annembed_analysis
cd annembed_analysis

### in the example input, column name or header will be skipped (detected automatically), the order of raws in output (most likely your sample) will be the same with that of the input.
## useage (v0.1.6 and later)
annembed --csv ./example/c-elegans_qc_final_all_2000.csv --scale 0.65 --nbsample 10 --stepg 2.0 --layer 0 --dim 2 -o fashion_embedded_csv.txt hnsw --dist 'DistL2' --nbconn 64 --ef 512 --knbn 15

### For high dimension datasets. We can use HubNSW (v0.1.8 or later) to reduce memory and speedup HNSW graph build
###get mist-fashion data (758 dimensions)
wget https://github.com/jianshu93/annembed/releases/download/v0.1.8/fashion-mnist_data.csv.gz
gunzip fashion-mnist_data.csv.gz
### scale_modify_f is to set number of layers to build, 0.25 is good to allow only 1 layer. 
annembed --csv ./fashion-mnist_data.csv --scale 0.65 --nbsample 10 --stepg 2.0 --layer 0 --dim 2 -o fashion_embedded.csv hnsw --dist 'DistL2' --nbconn 64 --ef 512 --knbn 15 --scale_modify_f 0.25
```

### Usage in Python
```bash
pip install annembed_rs
```
```python
import annembed, numpy as np
arr = annembed.embed("fashion-mnist_data.csv", dim=2)
print(type(arr), arr.shape)
arr1 = annembed.dmap_embed("fashion-mnist_data.csv", dim=2)
print(type(arr1), arr.shape)
```





By default, annembed will use all available computer cores/threads for nearly all steps except difussion map initialization, which is very fast even for large dataset. Annembed library can be found [here](https://github.com/jean-pierreBoth/annembed) or [here](https://crates.io/crates/annembed). Annembed can also be used as a library, as shown in the Ann section of [GSearch](https://github.com/jean-pierreBoth/gsearch)

### Output explanation
you will find a 2 column output embedded.csv by default, which are the embedded dimensions 1 and 2 respectively. Sample order are preserved and can be combined with sample metadata. Each run can be different because initialization is random and edge sampling is also random. But the visualization results will not be changed.

## Embedding genome database via [GSearch](https://github.com/jean-pierreBoth/gsearch) (install GSearch first)
```
### Install gsearch (Linux for example, see above for MacOS install)

https://github.com/jean-pierreBoth/gsearch/releases/download/v0.1.4/GSearch_Linux_x86-64_v0.1.3.zip
unzip GSearch_Linux_x86-64_v0.1.3.zip
cd GSearch_Linux_x86-64_v0.1.3
chmod a+x ./gsearch
./gsearch -h

### download pre-built bacterial genome HNSW graph database, check GSearch page ann section on how to do it
wget http://enve-omics.ce.gatech.edu/data/public_gsearch/GTDBv207_v2023.tar.gz
tar xzvf ./GTDBv207_v2023.tar.gz
cd ./GTDB/prot
tar xzvf k7_s12000_n128_ef1600.prob.tar.gz
gsearch ann -b ./k7_s12000_n128_ef1600_gsearch --stats --embed

```

The output of this step can be visualized, for example for the GTDB v207 we have the following plot. A new paper for the library and also this subcommand is in preparation.

![Alt!](https://github.com/jean-pierreBoth/gsearch/blob/master/GSearch-annembed-GTDBv207.jpg?raw=true)


### Performance note
By default, annembed use [Intel Math Kernel Library](https://www.intel.com/content/www/us/en/developer/tools/oneapi/onemkl.html) (intel-mkl-static feature) as the BLAS backend to make full use of x86 CPU performance on Linux machines. However, it is possible to use the open source [OpenBLAS](https://www.openblas.net) (openblas-static feature) as the BLAS backend. Our tests showed that OpenBLAS is slightly slower than Intel MKL on x86-64 Linux. On x86-64/Intel MacOS, OpenBLAS/Intel-MKL performance is significantly decreased compared to Linux but still supported (openblas-system/intel-mkl-system feature). We also provide the native BLAS framework support from MacOS called [Accelerate Framework](https://developer.apple.com/documentation/accelerate) (macos-accelerate feature). On aarch64 MacOS (M1, M2, M3 chips), only the OpenBLAS and Accelerate Framework backend is supported (macos-accelerate feature). Again, performance decreased for both compared to Linux. 


### Reference
Jianshu Zhao, Jean Pierre Both, Konstantinos T Konstantinidis, Approximate nearest neighbor graph provides fast and efficient embedding with applications for large-scale biological data, NAR Genomics and Bioinformatics, Volume 6, Issue 4, December 2024, lqae172, https://doi.org/10.1093/nargab/lqae172
