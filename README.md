# AutoTFCNNY
This repository contains the code and the data to train **AutoTFCNNY** model.

​    Contact: 1974887272@qq.com; solfix123@163.com

## Project Organization
      ├── AutoTFCNNY                     
         │
         │
         │     
         ├── README.md                   <- The README for users using AutoTFCNNY
         │
         │
         ├── Notebooks                   <- AutoTFCNNY  code for jupyter notebook. See README for their usages.
         │   ├── AutoTFCNNY.ipynb                      <- Training and predictions AutoTFCNNY models.
         │   ├── AutoTFCNNY-model.ipynb                <- Training  AutoTFCNNY models.
         │   ├── AutoTFCNNY-Test.ipynb                 <- Test AutoTFCNNY models.
         │   ├── Raw_data_processing.ipynb             <- Processing raw data 
         │   
         │ 
         │   
         │
         ├── Data                       <- Data for training and testing.See README for their usages.
         │   ├── BC
         │   ├── BL                   
         │   ├── BRCA                    
         │   ...
         │   ├── Health   
         │   ├── PCA15.txt  
         │   └── Example_raw_file.tsv        
         │
         ├── New Data                       <- New data set.See README for their usages.
         │   ├── BRCA
         │   ├── CRC
         │   ├── NSCLC
         │   ├── Melanoma               
         │   ├── UBC    
         │   ├── Health            
         |
         ├── Model                          <- Model for storing the optimal AutoTFCNNY
         |
         |
         ├── Model Test Files              <- Test model files for storing optimal AutoTFCNNY models
         │            
         │  
         ├── python_codes             <- Code for EarlyStopping  
         │            
         │ 
         ├── Result                         <- Experimental results of AutoTFCNNY
         |
         | 
         |── Compare and contrast models of notebooks   <- Compare the code of the model.
         │   ├── DeepLION.ipynb                     
         │   ├── DeepLION2.ipynb                
         │   ├── MINN-SA.ipynb                 
         │   ├── BiFormer.ipynb            
         │   ├── TransMIL.ipynb  
         │ 
         ├── AutoTFCNNY VS Deeplion             <- AutoTFCNNY experiments on the Deeplion dataset       
             ├── Notebooks                   <- AutoTFCNNY and Deeplion  code for jupyter notebook.
             │   ├── AutoTFCNNY-model.ipynb                <- Training  AutoTFCNNY models.
             │   ├── AutoTFCNNY-Test.ipynb                 <- Test AutoTFCNNY models.
             │   ├── Deeplion-model.ipynb                <- Training  Deeplion models.
             │   ├── Deeplion-Test.ipynb                 <- Test Deeplion models. 
             │
             ├── TrainingData                       <- Data for training .
             │   ├── Lung
             │   ├── THCA                   
             │   ├── PCA15.txt                         
             │
             ├── TestData                       <- Testdata set.See README for their usages.
             │   ├── Lung
             │   ├── THCA                                       
             |
             ├── Model Test Files                 <- Test model files for storing optimal AutoTFCNNY and Deeplion models
             │   ├── AutoTFCNNY
             │   ├── Deeplion                                       
             |             
             ├── python_codes             <- Code for EarlyStopping  
             │            
             │ 
             ├── Result                         <- Experimental results of AutoTFCNNY and Deeplion              
         
## Usage

### Python and essential packages

```
python         3.10.9
numpy          1.23.5
pandas         1.5.3
torch      2.0.1+cu117
```

### Input file format

The input files are tsv files in the following format:

```
TCR	Abundance
CATSDNSGGQPQHF	0.21069978688318255
CASSETGTYGYTF	0.034178689598235334
CASSYSSFSGELFF	0.01868772093003411
CASRTGGYGYTF	0.009927318418711613
CASSVLNTGELFF	0.009917718562069473
CASSLSVGPYEQYF	0.007108160518136263
CASSQGERGGNEQYF	0.006789231947469584
CASSAIRGVNTEAFF	0.006762565679019193
......
```

The sequences in the `TCR` column are the top 100 most abundant TCRs.

You can use the following command to extract TCR and its frequency information from raw files:

```
 jupyter notebook Raw_data_processing.ipynb 
 -----isource_dir = "../data/ Example_raw_file.tsv"  #Original file path
 -----output =  "../The path to the file you want to save/"  #Save the path to the processed file
```

### Predicting the cancer Index using pre-trained models

Prediction of all TCR files in a directory

```
 jupyter notebook AutoTFCNNY.ipynb 
 
 -----aa_file = "../Data/PCA15.txt"  #Amino acid characterization file path
 -----cancer_list =  ["BC","BL","UBC","BRCA","CC","CRC","DLBCL","GBM","HCC","Lung ADC","KS","Lung","MCC","Melanoma","MF","NSCLC","OS","OC","PDAC","PCa","RCC","SCLC"]  #Documentation of processed cancers
 -----data_dir = f'../Data/{Cancer_name}' #Cancers File Path
 ----- model_path = f'../Model/{Cancer_name}checkpoint{fold}.pt' #Save path of the model file
 
```

### Result

The metrics, accuracy, sensitivity, specificity, and area under the receiver operating characteristic (ROC) curve (AUC), are calculated and printed as:
``` 
  ————BC——————
Mean Accuracy (BC): 0.9665
Mean Sensitivity (BC): 1.0000
Mean Specificity (BC): 0.9486
Mean AUC (BC): 0.9991

```

### Model Testing and Evaluation

#### Train the model and save the best model file

```
 jupyter notebook AutoTFCNNY-Model.ipynb 
 
 -----aa_file = "../Data/PCA15.txt"  #Amino acid characterization file path
 -----Cancer_list = ["UBC","BRCA","NSCLC","Melanoma","CRC"] # Cancer
 -----data_dir = f'../Data/{Cancer_name}'   # Cancer File Path
 -----  model_path = f'../Model Test Files/{Cancer_name}checkpoint.pt' #Save path of the model file
 
```


#### Test the model

```
 jupyter notebook AutoTFCNNY-Test.ipynb 
 
 -----aa_file = "../Data/PCA15.txt"  #Amino acid characterization file path
 -----Cancers = ["UBC","BRCA","NSCLC","Melanoma","CRC"]     # Cancer 
 -----model_names = ["UBC","BRCA","NSCLC","Melanoma","CRC"]  # Cancer
 -----new_data_dir = f'../New Test Data/{Cancers_name}/' # New Test Set Path
 -----  model_path = f'../Model Test Files/{Cancer_name}checkpoint.pt' # model file
 
```



#### Result

The metrics, accuracy, sensitivity, specificity, and area under the receiver operating characteristic (ROC) curve (AUC), are calculated and printed as:
``` 
UBC - Accuracy: 0.9167, Sensitivity: 0.8333, Specificity: 1.0000, AUC: 0.9931
BRCA - Accuracy: 0.7174, Sensitivity: 0.4348, Specificity: 1.0000, AUC: 1.0000
NSCLC - Accuracy: 0.7009, Sensitivity: 0.4697, Specificity: 1.0000, AUC: 0.9923
Melanoma - Accuracy: 1.0000, Sensitivity: 1.0000, Specificity: 1.0000, AUC: 1.0000
CRC - Accuracy: 0.9000, Sensitivity: 0.8000, Specificity: 1.0000, AUC: 0.9800

```

