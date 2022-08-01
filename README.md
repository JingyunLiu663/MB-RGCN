# MB-RGCN

## Introduction
**M**ulti **B**ehavior - **R**esidual **G**raph **C**onvolutional **N**etwork (**MB-RGCN**) explicitly utilizes the ordinal relationship across behaviors with a lightweight model structure. Particularly, a chain of behavior blocks is used to explicitly encode the cascading behavior relationship with residual connections. In addition, LightGCN is applied to capture features for each behavior block, and a multi-task learning mechanism is leveraged to facilitate the model learning. 

## Environment
The MB-RGCN model is implemented under the following development environment:
- Python 3.6
- tensorflow==1.14.0
- scipy==1.5.4
- CUDA==11.0 
- numpy==1.19.5

## Datasets
- **Raw data**
  - Tmall: https://tianchi.aliyun.com/dataset/dataDetail?dataId=649
  
- **Preprocessed data**

  The preprocessed data can be found in the `/datasets` folder
 
## Files structure
1. python scripts

  a. `MB_RGCN.py`: This is the main structure of our MB-RGCN model, where we define the MB_RGCN recommender's class
  
  b. `Params.py`: This is the arguments available when running the `MB_RGCN.py` script. The arguments cover the dataset, model configurations and other hyperparameters
  
  c. `DataHandler.py`: This is the script used to load and process the pickled datasets, so that the main script can use the intermediate output to construct a recommender object for us
  
  d. Utils/: This is a folder with script serves the utility purposes
  
  -  `constants.oy`:
      
      This script covers the macros definition used in the project
    
   - `NNLayers.py`:
    
      This script covers functions for tensorflow parameters management, and the basic layers such as FC (fully connected) layer, dropout layer, normalization layers, etc., and basic functions such as activation functions for neural networks construction and training
    
  - `TimeLogger.py`:

      This script serves as the logging helper

## How to use the recommender model
1. Create a new folder named `History` in your working directory

```bash
mkdir History
```

2. Run the `MB_RGCN.py` script
- Beibei
```bash
python MB_RGCN.py --gcn_list 3 3 3
```

- Tmall
```bash
python MB_RGCN.py --gcn_list 4 4 4 4 --data tmall --save_path tmall_4444
```

### Parameters
- *gcn_list*: 
  
  The `gcn_list` argument cannot be skipped. You should use the long option argument `--gcn_list`, followed by a sequence of integers with space as the delimiter. The sequence of integers stands for the # of layers at **each behavior block**
  - for Beibei dataset, a integer sequence with a length of 3 shall be given, since the dataset comes with 3 behavior blocks by default
  - for Tmall dataset, a integer sequence with a length of 4 shall be given, since the dataset comes with 4 behavior blocks by default
- *data*: 

  The `data` argument indicates which dataset to use for training. By default, Beibei will be used.
  
- *save_path*:

  The `save_path` argument denotes the name of the training log file. In step 1, a working directory with the name `History` has been created, and the training log is saved under `History/` with a postfix of `.his`. If no save_path is given, the log file will be names as `tem` by default.
  
For the detailed information of other arguments available, please refer to the `Params.py` script. The nature of each argument has been well documented in the `help` arguments.

## References
- The main body of our code (The recommender constructor, train and test pipeline, and the data handler) refers to the code by 
- The implementation of the LightGCN layer refers to the official open source code of the original LightGCN paper.
