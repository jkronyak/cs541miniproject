# Note:
This repository contains code which is completely/almost completely adopted from the following source:  
https://github.com/geekyutao/RN  

This repository is utilized to host code which reproduces the results of the repository above.  
The original authors are: Tao Yu, Zongyu Guo, Xin Jin, Shilin Wu, Zhibo Chen, Weiping Li, Zhizheng Zhang, Sen Liu  

Steps for reproduction: 
1. Clone the repository.
2. Download the Places2 dataset (size 256 x 256), and the NVIDIA Irregular Mask Dataset (may have to resize to 256 x 256).
3. Generate the file lists (.flist) for the evaluation set. You will need to do this for masks and images. Make sure the .flist for the data and masks have the same number of files listed. I used 12,000 images and 12,000 masks. Samples of these files are eval_data.flist and eval_mask.flist. Use the following command to generate these: ``` python flist.py --path your_dataset_folder --output xxx.flist ``` 
4. Evaluate the model using eval.py. Here is the exact command and arguments I used to evaluate the pre-trained model:
``` 
python eval.py --gpus 1 --bs 14 --model pretrained_model/x_admin.cluster.localRN-0.8RN-Net_bs_14_epoch_3.pth --img_flist eval_data.flist --mask_flist eval_mask.flist --save_path output 
```  
There are several other options, such as specifying the number of gpus, etc. The original model used batch size 14, so I would recommend doing the same for the evaluation. Sample output is provided in the output.txt file. Note that specifying the --save_path parameter will create a folder which contains each image, each mask, each image with its mask applied, and the resulting reconstruction.
