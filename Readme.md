#Run remotely without installation or any other requirements
[https://astro.myftp.biz:62900/notebooks](https://astro.myftp.biz:62900/notebooks)
#Installation
## Required packages
* anaconda3
* Python 3.4
* Tensorflow
* Keras
* dicom, `$sudo pip install dicom`
* cell_magic_wand.py, included and is required to be in place of root directory with the notebooks 
* h5py `$sudo pip install h5py`

#The pipeline
1.	1ProcessNoduleDataset.ipynb
a.	Inputs: LIDC dataset (DOI folder), list3_2.csv, LIDC-IDRI_MetaData.csv
b.	Outputs: noduleimages.npy, nodulemasks.npy
2.	2TrainUnet.ipynb
a.	Inputs: noduleimages.npy, nodulemasks.npy
b.	Outputs: unet-weights-improvement.hdf5
3.	3ClassifyNodulesLIDC.ipynb
a.	Inputs: LIDC dataset (DOI folder), list3_2.csv, LIDC-IDRI_MetaData.csv, unet-weights-improvement.hdf5
b.	Outputs: truenodule-cnn-weights-improvement.hdf5
4.	4DetectNodules.ipynb
a.	Inputs: unet-weights-improvement.hdf5, truenodule-cnn-weights-improvement.hdf5, Kaggle DSB2017 dataset (stage1 folder), stage1_labels.csv, stage1_solution.csv
b.	Outputs: DSBNoduleImages\*.npy, DSBNoduleMasks\*.npy, DSBPatientNoduleIndex\*.csv 
5.	5CancerPredictionClassifiers.ipynb
a.	Inputs: DSBPatientNoduleIndex*.csv
6.	6CancerPredictionCNN.ipynb
a.	Inputs: DSBNoduleImages*.npy, DSBNoduleMasks*.npy, DSBPatientNoduleIndex*.csv
\*Split into a series of files due to large memory requirements

Run 