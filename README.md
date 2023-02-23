### MegaCRN: Meta-Graph Convolutional Recurrent Network

#### [AAAI23] R. Jiang*, Z. Wang*, J. Yong, P. Jeph, Q. Chen, Y. Kobayashi, X. Song, S. Fukushima, T. Suzumura, "Spatio-Temporal Meta-Graph Learning for Traffic Forecasting", Proc. of Thirty-Seventh AAAI Conference on Artificial Intelligence (AAAI), 2023. (Accepted to Appear)

#### Code and data are now available.
```bibtex
@article{jiang2022spatio,
  title={Spatio-Temporal Meta-Graph Learning for Traffic Forecasting},
  author={Jiang, Renhe and Wang, Zhaonan and Yong, Jiawei and Jeph, Puneet and Chen, Quanjun and Kobayashi, Yasumasa and Song, Xuan and Fukushima, Shintaro and Suzumura, Toyotaro},
  journal={arXiv preprint arXiv:2211.14701},
  year={2022}
}
```

#### Preprints
[![Arxiv link](https://img.shields.io/static/v1?label=arXiv&message=MegaCRN&color=red&logo=arxiv)](https://arxiv.org/abs/2211.14701)

#### Performance on Traffic Speed Benchmarks

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/spatio-temporal-meta-graph-learning-for/traffic-prediction-on-metr-la)](https://paperswithcode.com/sota/traffic-prediction-on-metr-la?p=spatio-temporal-meta-graph-learning-for)
[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/spatio-temporal-meta-graph-learning-for/traffic-prediction-on-pems-bay)](https://paperswithcode.com/sota/traffic-prediction-on-pems-bay?p=spatio-temporal-meta-graph-learning-for)
[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/spatio-temporal-meta-graph-learning-for/traffic-prediction-on-expy-tky-1)](https://paperswithcode.com/sota/traffic-prediction-on-expy-tky-1?p=spatio-temporal-meta-graph-learning-for)

#### Requirements
* Python 3.8.8 -> Anaconda Distribution
* pytorch 1.9.1 -> py3.8_cuda11.1_cudnn8.0.5_0
* pandas 1.2.4 
* numpy 1.20.1
* torch-summary 1.4.5 -> pip install torch-summary https://pypi.org/project/torch-summary/ (must necessary)
* jpholiday -> pip install jpholiday (not must, but if you want onehottime)

#### General Description
* The directory is structured in a flat style and only with two levels.
* The datasets are stored in DATA directories, and the model codes are put in model_DATA directories. 
* The training and testing function is merged into one file, we can just run "python traintest_MegaCRN.py" under each model directory.
* Also we can run "python MegaCRN.py" to simply check the model architecture without feeding the data.
* Also under model directory, metrics.py file contains the metric functions and utils.py file contains a set of supporting functions.

##### How to run our model (general command)?
* python generate_training_data.py --dataset=DATA
* cd model
* python traintest_MegaCRN.py --dataset=DATA --gpu=GPU_DEVICE_ID 
* DATA = {METRLA, PEMSBAY}
* For PEMSBAY dataset, please first upzip ./PEMSBAY/pems-bay.zip to get ./PEMSBAY/pems-bay.h5 file.
* You can also run two baselines GTS and GCRN similary.

##### How to run our model on EXPY-TKY?
* cd model_EXPYTKY
* python traintest_MegaCRN.py --dataset=DATA --gpu=GPU_DEVICE_ID 
* DATA = {EXPYTKY, EXPYTKY*} 
* EXPYTKY with 1843 links is the data used in our paper; EXPYTKY* is a superset of EXPYTKY that contains all 2841 expy-tky links.

#### Arguments
The default hyperparameters used in our paper are written in model/traintest_MegaCRN.py as follows.
The ratio for train:valid:test is roughly 7:1:2, generated by generate_training_data.py.
Please check the codes from parser = argparse.ArgumentParser().

##### Arguments (EXPY-TKY)
The hyperparameters for EXPY-TKY in model_EXPYTKY/raintest_MegaCRN.py are the same as the default except the following. EXPY-TKY data is structured by month, where '202110' and '202111' used as training and validation and '202112' used as testing. By further setting val_ratio as 0.25 (that meas 25% data of '202110' and '202111' as valid data), the ratio for train:valid:test is roughly 3:1:2. The time interval for EXPY-TKY is 10 minutes, thus observation/prediction horizon are both set to 6, to perform 1-hour-to-1-hour forecasting. </br>
