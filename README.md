# E3 Manifest

## Repo

```
mkdir -p ~/bin
export PATH=~/bin:$PATH
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```


## Init

* Create the working directory
```
mkdir E3_WORKING_DIRECTORY
cd E3_WORKING_DIRECTORY
```

* Initializes E3_WORKING_DIRECTORY to use the default.xml on the master branch

```
repo init -u https://github.com/jeonghanlee/manifest.git
```


* Initializes E3_WORKING_DIRECTORY to use a branch with groups
```
repo init -u https://github.com/jeonghanlee/manifest.git -b a_branch -g default,pkg,timing 
```

* Initializes E3_WORKING_DIRECTORY to use the test.xml, on the master branch
```
repo init -u https://github.com/jeonghanlee/manifest.git -m test.xml
```


## sync

```
repo sync
```