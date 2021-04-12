# Normalizing-Flows

**NOTE**: Model Weights (i.e. training logs) and the intermediate Cache can be found on this [Drive Link](https://drive.google.com/drive/folders/1kS9AJS2txirpITDypZBX2VP2xxd1cE0O?usp=sharing)

## Ideal Directory Structure

Directory Structure [Excluding Log/Temp Files]:
```
Normalizing-Flows
├── cache                                    # Available on Drive
│   ├── X_dict.pkl
│   ├── X_dict_0.pkl
│   ├── X_dict_1.pkl
│   ├── X_dict_2.pkl
│   ├── X_dict_3.pkl
│   └── X_dict_4.pkl
├── data                                     # Download Link Below
│   ├── Boosted_Jets_Sample-0.snappy.parquet
│   ├── Boosted_Jets_Sample-1.snappy.parquet
│   ├── Boosted_Jets_Sample-2.snappy.parquet
│   ├── Boosted_Jets_Sample-3.snappy.parquet
│   └── Boosted_Jets_Sample-4.snappy.parquet
├── get_dataset.py
├── logs                                     # Available on Drive
│   ├── ... model_1
│   ..
│   └── ... model_n
└── nbs
    └── task2.ipynb
```

## Parsed Images

![image](https://user-images.githubusercontent.com/34454784/114454383-30ed8800-9bf8-11eb-87f8-b4c2bbe651f3.png)
![image](https://user-images.githubusercontent.com/34454784/114454405-34810f00-9bf8-11eb-9353-ef0c8bb13221.png)
![image](https://user-images.githubusercontent.com/34454784/114454416-377bff80-9bf8-11eb-8ee1-db23c4115a75.png)

## Analysing Number of Instances in each channel
![image](https://user-images.githubusercontent.com/34454784/114454516-524e7400-9bf8-11eb-99b1-a73e972be78a.png)
![image](https://user-images.githubusercontent.com/34454784/114454458-4662b200-9bf8-11eb-8a34-2fd4191aae4d.png)
![image](https://user-images.githubusercontent.com/34454784/114454534-55e1fb00-9bf8-11eb-80cf-6a8dd6f3f439.png)


## Config File
```
# Defining various parameters.
cfg = {
    # Model Parameters
    'layers': [2048, 1024, 512, 256],   # Define the AutoEncoder Layers
    
    # DataLoader Parameters
    'batch_size': 1024,
    'num_workers': 32,

    # Training Parameters
    'device': torch.device('cuda:0'),   # Replace with 'cpu' if not using GPU.
    'learning_rate': 0.001,
    'optimizer': 'adam',
    'scheduler': None,                  # Example: 'ReduceLROnPlateau',
    'model_name': 'model1',
    'log_dir': 'logs',
    'checkpoint_count': 3,
    'callbacks': ['ModelCheckpoint']    # Example: ['ModelCheckpoint', 'EarlyStopping']   
}

# Config for PyTorch Lightning Trainer.
PyTorch_Lightning_Trainer_cfg = {
    'max_epochs' : 1000,
    'weights_summary' : None,
    'gpus': [0],                        # Replace with [] if not using GPU.
    'log_every_n_steps': 5,
    'check_val_every_n_epoch': 1
    
    ### Other Trainer settings ###
    # 'precision': 16
    # 'auto_lr_find': True,
    # 'overfit_batches' : 0.001, 
    # 'val_check_interval': 1.0,
    # 'limit_train_batches': 10,
    # 'limit_val_batches': 0,
    # 'progress_bar_refresh_rate': 0
}
```

## Training Logs (Tensorboard)

![image](https://user-images.githubusercontent.com/34454784/114454703-85910300-9bf8-11eb-921e-93133baaa744.png)
![image](https://user-images.githubusercontent.com/34454784/114454717-89248a00-9bf8-11eb-977e-1ab3e64e16b6.png)


## Analysis of EMD metric for Reconstructed Images

**Train Split**
```
RMSE Error : 24.799 ± 3.772
Average EMD: 0.970
```
![image](https://user-images.githubusercontent.com/34454784/114454804-9fcae100-9bf8-11eb-85a2-6a285fa5848a.png)

**Valid Split**
```
RMSE Error : 24.852 ± 4.020
Average EMD: 1.015
```
![image](https://user-images.githubusercontent.com/34454784/114454815-a2c5d180-9bf8-11eb-812c-a477480f1522.png)

**Test Split**
```
RMSE Error : 24.795 ± 4.021
Average EMD: 1.021
```
![image](https://user-images.githubusercontent.com/34454784/114454830-a6f1ef00-9bf8-11eb-9365-806fea7162e2.png)

## Comparision of Inputs and Reconstructions
![image](https://user-images.githubusercontent.com/34454784/114455013-e0c2f580-9bf8-11eb-89a0-135d2b4b035f.png)
![image](https://user-images.githubusercontent.com/34454784/114455020-e3254f80-9bf8-11eb-9923-8c72bd9cadff.png)
![image](https://user-images.githubusercontent.com/34454784/114455034-e7516d00-9bf8-11eb-89dc-029659e880ef.png)


## Resources and References
- Dataset: [Link](https://cernbox.cern.ch/index.php/s/xcBgv3Vw3rmHu9u)
- Analysis and approach inspired from the paper - "Graph Generative Models for Fast Detector
Simulations in Particle Physics" (Hariri et al., 2020) [[link](https://ml4physicalsciences.github.io/2020/files/NeurIPS_ML4PS_2020_138.pdf)]
- Cache and Logs: [Link](https://drive.google.com/drive/folders/1kS9AJS2txirpITDypZBX2VP2xxd1cE0O?usp=sharing)
```
