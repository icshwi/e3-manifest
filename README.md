E3 Manifest
===
[![Action Status](https://github.com/icshwi/e3-manifest/workflows/E3%20Building/badge.svg)](https://github.com/icshwi/e3-manifest/actions?workflow=E3+Building)

This repo is the pilot project in order to achieve how we duplicate the exact single point of E3 by using repo [[3]].  Thus, we evaluate this repo to use generic repo commands and E3 building make rules without introducing any other tools except command line commands. 



## Preparation

One needs to setup Repo as follows:

```
$ mkdir -p ~/bin
$ export PATH=~/bin:$PATH
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
$ chmod a+x ~/bin/repo
```


## Procedure

### Consideration

Note that one should not do this job frequently, after this, most of work will be done by individual modules. We may develop a better tool to setup it later.

### Step 1:  Create a directory
```
$ mkdir e3_env
$ cd e3_env
```

### Step 2: Init


* Initialize epics_env to use the default.xml [[4]] on the master branch

```
e3_env $ repo init -u https://github.com/icshwi/e3-manifest
```

### Step 3: Sync

```
e3_env $ repo sync --no-clone-bundle
```


### Step 4: Build

This step is only valid for the case when one would like to install E3 from scratch. The simple building rule is
```
cd a_specific_version_of_module_which_one_would_like_to_install
make init
make patch
make build
make install
```

#### BASE
From time to time, one should press `space` in one's keyboard. And then if one SEE `(END)`, type `esc` to return the console. 
```
e3_env $ repo forall -p --groups=base -c 'make init && make patch && make build'
```
OR
```
e3_env $ cd 0.epics-base/
0.epics-base ((7.0.3.1-NA/R-7.0.3.1-778a693-1911112218))$ make init
0.epics-base ((7.0.3.1-NA/R-7.0.3.1-778a693-1911112218))$ make patch
0.epics-base ((7.0.3.1-NA/R-7.0.3.1-778a693-1911112218))$ make build
0.epics-base ((7.0.3.1-NA/R-7.0.3.1-778a693-1911112218))$ cd ../
```

#### REQUIRE
```
e3_env $ repo forall -p --groups=require -c 'make init && make patch && make rebuild'
```
OR
```
e3_env$ cd 0.00.require/
0.00.require ((7.0.3.1-3.1.2/R-3.1.2-e0c84e4-1911121821))$ make init
0.00.require ((7.0.3.1-3.1.2/R-3.1.2-e0c84e4-1911121821))$ make patch
0.00.require ((7.0.3.1-3.1.2/R-3.1.2-e0c84e4-1911121821))$ make build
0.00.require ((7.0.3.1-3.1.2/R-3.1.2-e0c84e4-1911121821))$ make install
0.00.require ((7.0.3.1-3.1.2/R-3.1.2-e0c84e4-1911121821))$ cd ..
```
#### Common modules

```
e3_env$ repo forall --jobs=1 -p --groups=common -c 'make init && make patch && make rebuild'
```
OR
```
e3_env$ repo forall -p --groups=common -c 'make init >> ../common_init.log'
e3_env$ repo forall -p --groups=common -c 'make patch >> ../common_patch.log'
e3_env$ repo forall -p --jobs=1 --groups=common -c 'make build     >> ../common_build.log'
e3_env$ repo forall -p --jobs=1 --groups=common -c 'make install   >> ../common_install.log'
```

#### Timing modules
```
e3_env$ repo forall --jobs=1 -p --groups=timing -c 'make init && make patch && make rebuild'
```
OR
```
e3_env$ repo forall -p --groups=timing -c 'make init >> ../timing_init.log'
e3_env$ repo forall -p --groups=timing -c 'make patch >> ../timing_patch.log'
e3_env$ repo forall -p --jobs=1 --groups=timing -c 'make build     >> ../timing_build.log'
e3_env$ repo forall -p --jobs=1 --groups=timing -c 'make install   >> ../timing_install.log'
```

#### PSI modules
```
e3_env$ repo forall --jobs=1 -p --groups=PSI -c 'make init && make patch && make rebuild'
```
OR
```
e3_env$ repo forall -p --groups=PSI -c 'make init >> ../PSI_init.log'
e3_env$ repo forall -p --groups=PSI -c 'make patch >> ../PSI_patch.log'
e3_env$ repo forall -p --jobs=1 --groups=PSI -c 'make build     >> ../PSI_build.log'
e3_env$ repo forall -p --jobs=1 --groups=PSI -c 'make install   >> ../PSI_install.log'
```

#### IOxOS modules
Currently, few repositories need an access permission. Please contact us for the permission.
```
e3_env$ repo forall --jobs=1 -p --groups=ioxos -c 'make init && make patch && make rebuild'
```
OR

```
e3_env$ repo forall -p --groups=ioxos -c 'make init >> ../ioxos_init.log'
e3_env$ repo forall -p --groups=ioxos -c 'make patch >> ../ioxos_patch.log'
e3_env$ repo forall -p --jobs=1 --groups=ioxos -c 'make build     >> ../ioxos_build.log'
e3_env$ repo forall -p --jobs=1 --groups=ioxos -c 'make install   >> ../ioxos_install.log'
```

#### AreaDetector modules
```
e3_env$ repo forall --jobs=1 -p --groups=areaDetector -c 'make init && make patch && make rebuild'
```
OR
```
e3_env$ repo forall -p --groups=areaDetector -c 'make init >> ../areaDetector_init.log'
e3_env$ repo forall -p --groups=areaDetector -c 'make patch >> ../areaDetector_patch.log'
e3_env$ repo forall -p --jobs=1 --groups=areaDetector -c 'make build     >> ../areaDetector_build.log'
e3_env$ repo forall -p --jobs=1 --groups=areaDetector -c 'make install   >> ../areaDetector_install.log'
```

#### Ethercat modules
Note that one should install the etherlab master first. Please see the reference [[5]].
```
e3_env$ repo forall --jobs=1 -p --groups=ethercat -c 'make init && make patch && make rebuild'
```
OR
```
e3_env$ repo forall -p --groups=ethercat -c 'make init >> ../ethercat_init.log'
e3_env$ repo forall -p --groups=ethercat -c 'make patch >> ../ethercat_patch.log'
e3_env$ repo forall -p --jobs=1 --groups=ethercat -c 'make build     >> ../ethercat_build.log'
e3_env$ repo forall -p --jobs=1 --groups=ethercat -c 'make install   >> ../ethercat_install.log'
```



### Step 5: Set the E3
```
e3_env $ source /epics/base-7.0.3.1/require/3.1.2/bin/setE3Env.bash
e3_env $ iocsh.bash
```



## Additional commands

* Initialize a repo with a specific manifest file (for example `a_specific_manifest.xml`) on the master branch
```
repo init -u https://github.com/icshwi/e3-manifest -m a_specific_manifest.xml
```

* Force Sync
```
repo sync --force-sync --no-clone-bundle
```

## References and comments


(1) https://github.com/icshwi/e3                  
(2) https://github.com/icshwi/e3-manifest                     
(3) https://gerrit.googlesource.com/git-repo/                      
(4) https://raw.githubusercontent.com/icshwi/e3-manifest/master/default.xml                      
(5) https://github.com/icshwi/etherlabmaster                            



[1]: https://github.com/icshwi/e3                  
[2]: https://github.com/icshwi/e3-manifest                     
[3]: https://gerrit.googlesource.com/git-repo/                      
[4]: https://raw.githubusercontent.com/icshwi/e3-manifest/master/default.xml                      
[5]: https://github.com/icshwi/etherlabmaster                            

