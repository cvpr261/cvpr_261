# Code for CVPR 261 Submission


### Requirements
* Python >= 3.7
* Pytorch >= 1.7.0
* CUDA>=10.2
* Training Data
  
  Download [C-Driving Dataset](https://drive.google.com/drive/folders/1VXwbSKJnGO8etXy7H8GUjAjSIN5ddlcv?usp=sharing). Unzip the dataset and ensure the file structure is as follow:

  ```
  C-Driving
  ├── list
  ├── train
  │   ├── compound
  │   │   ├── cloudy
  │   │   ├── rainy
  │   │   └── snowy
  │   ├── open_not_used
  │   │   └── overcast
  │   └── source
  └── val
      └── compound
          ├── cloudy
          ├── rainy
          ├── snowy
          └── overcast
  ```
  **Note**: We move the overcast validation directory into the compound directory for calculating the averaged mIoU of compound and open domains.

### Run
* **Stage I**. Download [ImageNet pre-trained model](https://drive.google.com/drive/folders/1VXwbSKJnGO8etXy7H8GUjAjSIN5ddlcv?usp=sharing) and save it in `pretrain/vgg16-00b39a1b-updated.pth`
  
  * Train stage I.
    ```
    python train.py --cfg configs/train_source.yml
    ```
  * Test stage I.
    ```
    python test.py --cfg configs/train_source.yml
    ```

* **Stage II**. This stage requires the well-trained model from stage I as the pre-trained model. You can get it by testing the stage I or download [the source training model](https://drive.google.com/drive/folders/1VXwbSKJnGO8etXy7H8GUjAjSIN5ddlcv?usp=sharing) and save it in `pretrain/source_trained_model.pth`
  
  * Train stage II.
    ```
    python train.py --cfg configs/train_target.yml
    ```
  * Test stage II.
    ```
    python test.py --cfg configs/train_target.yml
    ```

<!-- You can also download the above models from [Baidu Drive](https://pan.baidu.com/s/1bYC-ohq5oR7VZ5mxQZe1Uw) (password: 6vg2). -->

### Inference

You can download the trained models in the paper from [Google Drive](https://drive.google.com/drive/folders/1VXwbSKJnGO8etXy7H8GUjAjSIN5ddlcv?usp=sharing). Change the `TEST.RESTORE_FROM` in `model_testing.yml` and then run the command
```
python test.py --cfg configs/model_testing.yml
```
