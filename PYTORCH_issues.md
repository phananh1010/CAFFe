This installation approach allows you to install Pytorch and related packages in your local directory. No admin permission required. The only requirement is conda has been installed into the system.

Conda is one of the most convinient way to install pytorch. If you have conda in your system, then installing Pytorch is just in few steps. 

Step1: create & activate conda environment:

```
conda create -n env_torch python=2.7
conda activate env_torch
```

Step 2: install pytorch packages

`conda install pytorch-cpu torchvision-cpu -c pytorch`

Step 3: check environment path to see if the packages have been installed

```
conda list
which python
```

Note: 
- Recently, conda automatically activate base environment. This maybe annoying since your environment path will be overrided by the base environment.
To force conda to use your customize environment path, use the following command:
`conda config --set auto_activate_base false`
- If you want your environment to be added into yupiter notebook, use following command (ipykernel packge required):
```
source activate env_pytorch
python -m ipykernel install --user --name env_pytorch --display-name "Python (env_pytorch)"
```

