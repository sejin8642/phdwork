## Introduction
This git repository is created to store frozen codebase of my PhD research project. All the information on how to use the code is written as comments and docstrings within the python scripts.

## Dependencies
To run the code, you must install Python of version 3.7 or higher, Numpy, Scipy, and TensorFlow. In order to use accelerated Nvidia GPU, please install TensorFlow with cudnn.

## ftnmr
ftnmr module contain classes for creating molecule and spectrometer. There are also other functions and classes to facilitate dynamic programming in my project. The following code snippet shows ftnmr use cases
```python
# ftnmr.molecule contains hydrogen groups with the total number and chemical shift.
# Based on J-coupling constants, spectral splits with their distribution is also created
hydrogens={'a':(12, 0.0, 120.0), 'b':(6, 0.0, 180.0)}
couplings = [('a', 'b', 10)]
molecule = ftnmr.molecule(hydrogens=hydrogens, couplings=couplings) 

# create a spectrometer object
spec = ftnmr.spectrometer() 

# solution dict with the above molecule whose relative abundance is 12
moles = {'A':(molecule, 12)}

# measure and process NMR signal with baseline distortion artifact
spec.artifact(baseline=True)
spec.measure(moles=moles)
spectra, target = spec() # returns the original (with artifact) and target spectra
```

## projnmr
projnmr module contain a class that can generate random molecule for data simulation.
```python
# returns ftnmr.molecule object
molecule = projnmr.metaboliteGenerate() # 
```

## SLURM scripts: gend and train_model
The template scripts for data simulation and training the model. Please change the parameters accordingly to get the type of data you want and to train the model with your choice of hyperparameters and training parameters (all the parameters are commented and have docstrings in the code for anyone to understand). The scripts are written specifically for sbatch command on HPC setup.
```
sbatch gend.py
sbatch train_model.py
```

## Questions
If any part of the code does not make any sense, please contact at sejinnam@hawaii.edu for help.

