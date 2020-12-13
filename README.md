# differentiable_filters
tensorflow (1.14) code for the paper "How to train your differentiable filter". 

Implements the Extended Kalman filter, the Unscented Kalman filter, a sampling based Unscented Kalman filter and the Particle filter as differentiable recurrent network layers. 

## Disclaimer: Work in progress
This initial release mainly contains the code as it was used to produce the results in the paper. Upcoming releases will include an easier-to-use minimal example and a port to tensorflow 2. 

## Installation:

You can either use 
```
pip3 install .
```
or 
``` 
python3 setup.py install
```

## Usage

First create a dataset, e.g.

```
create_toy_dataset --out-dir=[path/to/data] --num-examples=100
```
This will create a small dataset for the simulated disc tracking task named "toy_pn=0.1_d=5_const", i.e. a set with constant process noise (sigma_p = 0.1) and 5 distractor discs.

Now create a directory for the output of the training somewhere. Then, run for example
```
run_filter_experiment --name=my_first_df --problem=toy --filter=ekf --data-name-train=toy_pn=0.1_d=5_const --data-dir=[path/to/data] --out-dir=[path/to/output] --pretrain-process=1 --pretrain-observations=0 --scale=100 --hetero-r=1 --hetero-q=0
```
This will train a differentiable EKF with heteroscedastic observation noise (hetero-r=1) and constant process noise (hetero-q=0). pretrain-process=1 defines that a pretrained process model should be used. By default, the pretrained process noise will not be used (to do so, set use-pretrained-covar=1). If no trained model is available, the pretraining will be done automatically. scale=100 downscales the complete state-space by a factor of 100, which we found empirically useful. 

## Author:
Alina Kloss

Copyright(c) 2020 Max Planck Gesellschaft

See LICENSE for license details.
