E3 Manifest : The single point release method
===
[![Action Status](https://github.com/icshwi/e3-manifest/workflows/E3%20Building/badge.svg)](https://github.com/icshwi/e3-manifest/actions?workflow=E3+Building)

This repo is the pilot project in order to achieve how we duplicate the exact single point of E3 by using repo [[3]].  Thus, we evaluate this repo to use generic repo commands and E3 building make rules without introducing any other tools except command line commands. 

## Requirements

The all E3 module repositories should be selected by a tag or git hash id. They are used to build a E3 manifest file. Each repository has its own corresponding BASE and REQUIRE versions in its `RELEASE` file. 

## Possible Scenario


* `T=t0` : We first setup the production E3 environment
* `T=t1` : We add the master branch of stream module into the existent production E3 environment
* `T=t2` : We upgrade the require version
* `T=t3` : One In-kind would like to duplicate `T=t1` E3 in their institute. 

However, once we move the different base, require, or both versions, it is much better to move a brand-new manifest file. We can run one by one according to its time order. 

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

```
e3_env $ repo forall --groups=base -c 'make init && make patch && make build'
```
OR
```
e3_env $ cd 0.epics-base/
0.epics-base ((7.0.3.1-NA/R-7.0.3.1-778a693-1911112218))$ make init
0.epics-base ((7.0.3.1-NA/R-7.0.3.1-778a693-1911112218))$ make patch
0.epics-base ((7.0.3.1-NA/R-7.0.3.1-778a693-1911112218))$ make build
0.epics-base ((7.0.3.1-NA/R-7.0.3.1-778a693-1911112218))$ cd ../
```
Note that `make all` does not exist for BASE.

#### REQUIRE

```
e3_env $ repo forall --groups=require -c 'make init && make patch && make rebuild'
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
OR

```
e3_env $ repo forall --groups=require -c 'make all'
```
#### Common modules

```
e3_env$ repo forall --jobs=1 --groups=common -c 'make all'
```

#### Timing modules
```
e3_env$ repo forall --jobs=1 --groups=timing -c 'make all'
```

#### PSI modules 
Note that Common modules group should be installed before. 
```
e3_env$ repo forall --jobs=1 --groups=PSI -c 'make all'
```

#### IOxOS modules
Note that Common modules group should be installed before. And currently, few repositories need an access permission. Please contact us for the permission.
```
e3_env$ repo forall --jobs=1 --groups=ioxos -c 'make all'
```

#### AreaDetector modules
Note that Common modules group should be installed before. 
```
e3_env$ repo forall --jobs=1 --groups=areaDetector -c 'make all'
```

#### Ethercat modules
Note that one should install the etherlab master first. Please see the reference [[5]]. And Note that Common modules group should be installed before. 
```
e3_env$ repo forall --jobs=1 --groups=ethercat -c 'make all'
```

### Step 5: Set the E3
```
e3_env $ source /epics/base-7.0.3.1/require/3.1.2/bin/setE3Env.bash
e3_env $ iocsh.bash
```



## Additional commands

### Output messages will be redirected
One needs to type `space` key from time to time in order to see all outputs such as stdin, stdout, stderr.

```
e3_env$ repo forall --jobs=1 -p --groups=ethercat -c 'make init && make patch && make -s rebuild'
```
### Initialize a repo with a specific manifest file
```
repo init -u https://github.com/icshwi/e3-manifest -m a_specific_manifest.xml
```

### Force Sync
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

