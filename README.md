<div align="center">
  <img width="50%" src ="Annembed_logo.jpg">
</div>

# Scripts for reproducing [annembed](https://crates.io/crates/annembed) paper
## All scripts are in the scripts folder to directly produce figures in the paper
###
This is a colloboration between [Jianshu Zhao](https://github.com/jianshu93) and [Jean Pierre-Both](https://github.com/jean-pierreBoth) (algorithm part). In the scripts folder, you can see the R scripts used to reproduce the main figures in the paper. 

### Simple case for install

```bash
conda install -c bioconda -c conda-forge annembed
```


```
### Linux
wget https://github.com/jianshu93/annembed/releases/download/v0.1.6/annembed_Linux_x86-64_v0.1.6.zip
unzip annembed_Linux_x86-64_v0.1.6.zip
chmod a+x ./annembed
./annembed -h

### Macos
wget https://github.com/jianshu93/annembed/releases/download/v0.1.6/annembed_universal.tar.gz
tar -xzvf ./annembed_universal.tar.gz
chmod a+x ./annembed
### check install MacOS, you may need to change the system setup to allow external binary to run by type the following first and use your admin password
sudo spctl --master-disable
./annembed -h

### or you can have Homebrew on MacOS installed first then (recommended):
brew update
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

### in the example input, column name or header will be skipped (detected automatically), the order of raws in output (most likely your sample) will be the same with that of the input.
annembed --csv ./example/C_elegan_embedded_try.csv embed --scale 0.65 --nbsample 10 --stepg 2.0 --layer 0
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
Zhao et.al., 2024,Approximate Nearest Neighbor Graph Provides Fast and Efficient Dimension Reduction with Applications for Large-scale Biological Data [bioRxiv](https://www.biorxiv.org/content/10.1101/2024.01.28.577627v1)
