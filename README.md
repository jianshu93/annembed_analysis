# Scripts for reproducing annembed paper
## All scripts are in the scripts folder to directly produce figures in the paper
###
In the scipts folder, you can see the R scripts used to reproduce the main figures in the paper.

### Simple case for install
```
### Linux
wget https://github.com/jianshu93/annembed/releases/download/v0.1.0/annembed_Linux_x86-64.zip
unzip annembed_Linux_x86-64.zip
chmod a+x ./annembed
./annembed -h

### Macos
wget https://github.com/jianshu93/annembed/releases/download/v0.1.0/annembed_universal.tar.gz
unzip annembed_universal.tar.gz
chmod a+x ./annembed
### check install MacOS, you may need to change the system setup to allow external binary to run by type the following first and use your admin password
sudo spctl --master-disable
./annembed -h

### or you can have Homebrew installed first then:
brew tap jianshu93/annembed
brew install annembed
annembed -h

```

### Usage
Annembed can be run like this (see the example input format): 
```
annembed-new --csv ./c-elegans_qc_final_all.csv embed --scale 0.6 --nbsample 10 --stepg 2.0 --layer 0
```
By default, annembed will use all available computer cores/threads for nearly all steps. Annembed library can be found here: https://crates.io/crates/annembed . Annembed can also be used as a library, as shown in the GSearch program (Ann section) (https://github.com/jean-pierreBoth/gsearch)
