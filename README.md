# E3 Manifest

European Spallation EPICS Environment (E3) [[1]] Deployment.



## Preparation

One needs to setup Repo as follows:

```
$ mkdir -p ~/bin
$ export PATH=~/bin:$PATH
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
$ chmod a+x ~/bin/repo
```


## Procedure

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
```
e3_env $ 

```

### Step 5: Set the E3
```
e3_env $ 
```



## Platform Path
In the directory, one can find the following additional tools which allow users to install few more enviornment or libraries. For further information, please look at corresponding urls:

### ethercat
* https://github.com/icshwi/etherlabmaster

### lmfit
* https://github.com/jeonghanlee/lmfit-env

### opencv
* https://github.com/jeonghanlee/opencv-env

### nioc
* https://github.com/jeonghanlee/epics_NIOCs



## Additional commands

* Initialize epics_env to use the epics_180811.xml, on the master branch
```
repo init -u https://github.com/icshwi/e3-manifest -m e3-180801.xml
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
(5) https://raw.githubusercontent.com/icshwi/e3/master/tools/use_sshkey.sh                      
(6) https://github.com/icshwi/etherlabmaster                            



[1]: https://github.com/icshwi/e3                  
[2]: https://github.com/icshwi/e3-manifest                     
[3]: https://gerrit.googlesource.com/git-repo/                      
[4]: https://raw.githubusercontent.com/icshwi/e3-manifest/master/default.xml                      
[5]: https://raw.githubusercontent.com/icshwi/e3/master/tools/use_sshkey.sh                      
[6]: https://github.com/icshwi/etherlabmaster                            

