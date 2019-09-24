# Input-Cell Attention
Code implementing architecture introduced in "Input-Cell Attention Reduces Vanishing Saliency of Recurrent Neural Networks" by
Aya Abdelsalam Ismail, Mohamed Gunady, Luiz Pessoa, Hector Corrada Bravo*, Soheil Feizi*.

![alt text](Images/cellAttentionLstm.png)

## Overview:
Recent efforts to improve the interpretability of deep neural networks use saliency to characterize the importance of input features in predictions made by models. Work on interpretability using saliency-based methods on Recurrent Neural Networks (RNNs) has mostly targeted language tasks, and their applicability to time series data is less understood. In this work we analyze saliency-based methods for RNNs, both classical and gated cell architectures. We show that RNN saliency vanishes over time, biasing detection of salient features only to later time steps and are, therefore, incapable of reliably detecting important features at arbitrary time intervals. To address this vanishing saliency problem, we propose a novel RNN cell structure (input-cell attention), which can extend any RNN cell architecture. At each time step, instead of only looking at the current input vector, input-cell attention uses a fixed-size matrix embedding, each row of the matrix attending to different inputs from current or previous time steps.  Using synthetic data, we show that the saliency map produced by the input-cell attention RNN is able to faithfully detect important features regardless of their occurrence in time. We also apply the input-cell attention RNN on a neuroscience task analyzing functional Magnetic Resonance Imaging (fMRI) data for human subjects performing a variety of tasks. In this case, we use saliency to characterize brain regions (input features) for which activity at specific time intervals is important to distinguish between tasks. We show that standard RNN architectures are only capable of detecting important brain regions in the last few time steps of the fMRI data, while the input-cell attention model is able to detect important brain region activity across time without latter time step biases. 

##Prerequisites:

##Usage
The code is available under scripts folder
### Synthetic Data creation:
```python createSimulationData.py```

cd Scripts
python createSimulationData.py --DataName TopBox           --NumTrainingSamples 1000 --NumTestingSamples 300 --NumTimeSteps 100 --NumFeatures 100 --ImpTimeSteps  30 --ImpFeatures  80 --StartImpTimeSteps 0 --EndImpTimeSteps 30 --StartImpFeatures 10 --EndImpFeatures  90 --multipleBox False
1. createSimulationData.py --> Creates TopBox,MiddleBox,BottomBox,ThreeUpperBoxes,ThreeMiddleBoxes datasets to choose which dataset to create uncomment it in the code
2. createMixedSimulationData.py --> Creates MixedBoxes Dataset.
3. createMovingSimulationData.py --> Creates datasets for moving boxes experiments
Datasets will be saved in Data folder
## Train Models:
- Uses trainLSTMModels.py
- Uncomment the model you would like to train and write the dataset details in the arguments
- Models will be in Models folder
## Create Saliency:
- Uses vanillaSaliencyClean.py
- Uncomment the model you would like to train and write the dataset details in the arguments'
- Saliencies and gradients will be saved in Results folder
## Get Statics:
-  To get table used in the paper uses BoxStat.py it reads from Salincy from Results folder. (uncomment the desired models)
-  To get plot for moving boxes:
    1. Run MovingBoxStat.py
    2. Run MovingBoxPlot.py
