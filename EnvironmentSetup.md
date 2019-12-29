## Environment setup

### Prerequisites
1. `pip`
If you don't have `pip`,  you can download and install it using instructions [here](https://pip.pypa.io/en/stable/installing/). 
To test if you have `pip` successfully installed, in the command line type: 
```
which pip
```
You should see output that looks like this: 
```
/Library/Frameworks/Python.framework/Versions/3.7/bin/pip
``` 

2. `pipenv`
Install `pipenv` by running on the command line:  
```
pip install --user pipenv
``` 
To test correctly installed, type: 
```
pipenv --version
```
You should see some output like: 
```
pipenv, version 2018.11.26
```
If you have issues, check [here](https://pip.pypa.io/en/stable/user_guide/#user-installs) for help. 

3. `bazel`
Follow instructions from original exoplanet github repo to install `bazel`. 
___
### Directory setup
I have my directory set up as follows, this isn't necessary but keeping the Pipfile/lock file out of the actual code helps to keep things clean. 
```
my_exoplanet_project
│  Pipfile (more info below)
│  Pipfile.lock (will be created later)
│  README.md*
|  AUTHORS*
|  LICENSE*
└───exoplanet-ml*
│   │   WORKSPACE*
│   │   all the other exoplanet code downloaded from github*
```
All files with * are downloaded straight from the exoplanet github. 
___
### Pipfile
The Pipfile tells your virtual python environment which packages are going to be installed. 
You can find a pre-created Pipfile that has all the packages with the versions pre-determined for use with this project [here](https://github.com/caitlynlee/exoplanet-ml/blob/master/Pipfile). You can just download and use it as is. 

The Pipfile is configured for **Python 3.7**. If you want to use a different version of Python (2.7, 3.6) , just change the `python_version` in line 19 to whichever version you want to use. Make sure there's no extension on the file (.txt, .rtf, etc.) after you're done editing. 

Once you've downloaded the Pipfile and placed it into the directory where you want it (or if you want to just to start by creating your own), if you want to **add** packages to the Pipfile (now or whenever), go into the directory containing the Pipfile and type: 
```
pipenv install [packagename] 
```
If you're not going to download/use the `Pipfile` provided at the link above, you need to go in and manually add all the necessary packages as listed [here](https://github.com/google-research/exoplanet-ml/blob/master/README.md#required-packages). **Install tensorflow==1.15** if you're manually adding. 

This will install the package and create a `Pipfile.lock` file. 

If you don't want to add any packages and are just using the existing `Pipfile`, before activating the virtual environment you must type: 
```
pipenv install
```
This will install all the packages and create the `Pipefile.lock` from the existing packages listed in the `Pipfile`. 
___
### Activate virtualenv
If the packages were all installed successfully, you should see a prompt that tells you to activate the virtualenv. Do so by typing: 
```
pipenv shell
```
Successful output looks like: 
```bash
Launching subshell in virtual environment…

bash-3.2$  . /Users/leecaitl/.local/share/virtualenvs/my_exoplanet_project-mcaQ6OM1/bin/activate

(my_exoplanet_project)bash-3.2$
```
You've created the virtual env and are ready to work within it! 
`cd` into the exoplanet directory as you probably won't be needing to do anymore work at the top level. 
___
### Necessary Code changes 

1.  In *light_curve/BUILD*, line 74 needs to be changed to `cc_proto_library` and lines 71 and 76 (the `api_version` attributes need to be deleted) 

After this change, you should be able to `build` successfully. As a sanity check you can run
```
bazel build astronet/... astrowavenet/... light_curve/... tf_util/... third_party/...
```
You can also just keep going because running unit tests will start by building all the packages if they're not already built. 
2. `Astronet/ops/dataset_ops_test.py`   
Update dataset path. line 231: 
```self._file_pattern = _TEST_TFRECORD_FILE```  
3. `Astrowavenet/data/base_test.py`   
Update dataset path. line 108:  
```self._file_pattern = _TEST_TFRECORD_FILE```

Now you should be able to test by running: 
```
bazel test astronet/... astrowavenet/... light_curve/... tf_util/... third_party/...
```

You should have all the unit tests passing! Happy planet hunting
___
### Other notes
1. To exit the virutalenv, just type `exit` on the command line in the environment and it'll be closed out. 
2. If you update any of the packages in the `Pipfile` at any point, make sure you've re-installed and the `Pipfile.lock` is up to date. You can type `pipenv install` to double check if you're not sure. 
3. To clean up the `bazel` package cache and re-build/re-test without the cache, you can run `bazel clean` from within the exoplanet directory and it should remove all the *bazel-...* directories. 
