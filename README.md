# Segmentation of Lung Lobes and Lesions in Chest   CT for the Classification of COVID-19 Severity
Video: https://youtu.be/bAVM-OChI_k

<img src="https://github.com/hds-69/csc-app/blob/2abecc4e249e88afafad68fa137d6251f2a77d0b/Project%20info/framework.gif" style="max-width: 20%;" align="center" />

## About
To precisely determine the severity of COVID-19-related pneumonia, computed tomography (CT) is an imaging modality beneficial for patient monitoring and therapy planning. Thus, we aimed to develop a deep learning-based image segmentation model to automatically assess lung lesions related to COVID-19 infection and calculate the total severity score (TSS). The entire dataset consists of 100 COVID-19 patients acquired from Chulabhorn Hospital, divided into 25 cases without lung lesions and 75 cases with lung lesions categorized severity by radiologists regarding TSS. The model combines a 3D-UNet with pre-trained DenseNet and ResNet models for lung lobe segmentation and calculation of the percentage of lung involvement related to COVID-19 infection as well as TSS measured by the Dice similarity coefficient (DSC). Our final model, consisting of 3D-UNet integrated with DenseNet169, achieved segmentation of lung lobes and lesions with Dice similarity coefficients of 0.929 and 0.842, respectively. The calculated TSSs are similar to those evaluated by radiologists, with an R2 of 0.833. The correlation between the ground-truth TSS and model prediction was greater than that of the radiologist, which was 0.993 and 0.836, respectively.

App demo: please use in local computer.

## Requirements
1. You need install `Python >= 3.9.13`
2. Library requirement

        streamlit
        numpy
        pandas
        patchify==0.2.3
        segmentation-models-3D==1.0.3
        keras==2.8.0
        Keras-Applications==1.0.8
        tensorflow==2.8.0
        regex
        scikit-image==0.18.3
        pandas==1.3.5
        matplotlib
        numba
        zipp
        opencv-python==4.5.5.64
        Pillow==8.3.2
        fpdf

## Installation
1. clone this project followed by Github CLI command: 

       gh repo clone hds-69/csc-app
   or download project `zip` file 
2. Open a command prompt or terminal for `CD` command to change the directory to project location.
3. Installation with pip allows the usage of the install command:

        pip install -r requirements.txt
        
4. Run the App

        streamlit run app.py

## Use steps
Installation handbook: [https://docs.google.com/presentation/d/1DoHhD1M588GQGURy2NagAL8hC8nkRoxNFfkGxB3L2vs/edit?usp=sharing](https://github.com/hds-69/csc-app/blob/70d2c9619397a46d69f06923292e4f6a94cb819d/Document/Manual.pdf)

1. Input Lung CT-scan image `.jpg` (Min/Max range  80-256 images per patient)
<img src="https://github.com/hds-69/csc-app/blob/f5f5645ab9675d7b73a79cc297e26cf8fa5ec60f/Project%20info/upload.gif" style="max-width: 20%;" align="center" />

2. Click `Predict` button.
<img src="https://github.com/hds-69/csc-app/blob/57db1150b52154eb33c64af3959c8c43b697c35b/Project%20info/predict.gif" style="max-width: 20%;" align="center" />

3. Click `Save` button.
<img src="https://github.com/hds-69/csc-app/blob/57db1150b52154eb33c64af3959c8c43b697c35b/Project%20info/save.gif" style="max-width: 20%;" align="center" />

## Development process
1. Dataset: Train 32 cases (3,752 images), Test1 8 cases (1,314 images), Test2 62 cases (7,686 images)

   CT-scans image range: `92-208` images
   
   Case Type: `No lesion, Mild, Moderate, Severe`
   
2. Image Annotation by labelme for using label mask for Model Training. (for Train set and Test1 set)
3. Traning Model: 3D-Unet + Backbone (DenseNet, ResNet) using API: https://github.com/ZFTurbo/segmentation_models_3D
4. Model Evaluation with Test1 dataset.
5. User Interface (UI) Development using Streamlit.
6. Develop the Percentage of Infection (PI%) and TSS calculation.
7. TSS Evaluation with Test2 dataset.

## Results
The model was evaluated on a dataset of 8 infected patients, and the results demonstrated that 3D-UNet + DenseNet169 achieved the best performance, yielding Dice Similarity Coefficient (DSC) of `92.89%` and `84.22%` for lung lobe and lesion segmentation, respectively. The proposed model can reliably segment lesions on CT scans of severe cases, but the model performed less accurately in segmenting lung lesions of mild and moderate cases. However, the TSS calculated by the proposed model were comparable to those assigned by radiologists. Using CT scans of 62 COVID-19 patients for evaluation, the correlation coefficient (r) was `0.9125`, indicating a very strong correlation.

Model Testing Result Table `Test with Test set 1`

| Objective             | Model   | Backbone   | IoU  |  DSC | Accuracy | Precision | Sensitivity | Specificity |
| --------------------- | ------- | ----------- |------|------|----------|-----------|-------------|-------------|
| Lung lobe segmentation| 3D-Unet |DenseNet 169 |90.44%|92.89%| 98.49%   | 94.18%    | 95.52%      | 98.49%      |
| Lesion segmentation   | 3D-Unet |DenseNet 169 |79.61%|84.22%| 98.86%   | 86.7%     | 89.07%      | 98.91%      |


TSS calculation Testing Result Table `Test with Test set 2`
| Regression Statistics  | Value   |
| ---------------------- | ------- |
| Correlation Coefficient| 0.9125  |
| R Square               | 0.8327  |
| Adjusted R Square      | 0.8299  |
| Standard Error         | 2.5629  | 
| Observations           |   62    |
| p-value                | <0.001   |


## Citation

For more information, kindly acknowledge our project by citing it when using the code. The article is currently under review.
```
Prachaya Khomduean, Pongpat Phuaudomcharoen, Totsaporn Boonchu et al.
Segmentation of Lung Lobes and Lesions in Chest CT for the Classification of COVID-19 Severity,
19 January 2023, PREPRINT (Version 1) 
available at Research Square [https://doi.org/10.21203/rs.3.rs-2466037/v1]
```
