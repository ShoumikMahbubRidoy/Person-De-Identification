<p align="center"><img width="40%" src="jpg/logo.jpg" /></p>

--------------------------------------------------------------------------------
This repository provides a PyTorch implementation 

<p align="center"><img width="100%" src="jpg/main.jpg" /></p>


## Dependencies
* [Python 3.5+](https://www.continuum.io/downloads)
* [PyTorch 0.4.0](http://pytorch.org/)
* [TensorFlow 1.3+](https://www.tensorflow.org/) (optional for tensorboard)


<br/>

## Usage

### 1. Cloning the repository
```bash
$ git clone https://github.com/yunjey/StarGAN.git
$ cd StarGAN/
```

### 2. Downloading the dataset
To download the CelebA dataset:
```bash
$ bash download.sh celeba
```

To download the RaFD dataset, you must request access to the dataset from [the Radboud Faces Database website](http://www.socsci.ru.nl:8180/RaFD2/RaFD?p=main). Then, you need to create a folder structure as described [here](https://github.com/yunjey/StarGAN/blob/master/jpg/RaFD.md).

### 3. Training
To train StarGAN on CelebA, run the training script below. See [here](https://github.com/yunjey/StarGAN/blob/master/jpg/CelebA.md) for a list of selectable attributes in the CelebA dataset. If you change the `selected_attrs` argument, you should also change the `c_dim` argument accordingly.

```bash
$ python main.py --mode train --dataset CelebA --image_size 128 --c_dim 5 \
                 --sample_dir stargan_celeba/samples --log_dir stargan_celeba/logs \
                 --model_save_dir stargan_celeba/models --result_dir stargan_celeba/results \
                 --selected_attrs Black_Hair Blond_Hair Brown_Hair Male Young
```

To train StarGAN on RaFD:

```bash
$ python main.py --mode train --dataset RaFD --image_size 128 --c_dim 8 \
                 --sample_dir stargan_rafd/samples --log_dir stargan_rafd/logs \
                 --model_save_dir stargan_rafd/models --result_dir stargan_rafd/results
```

To train StarGAN on both CelebA and RafD:

```bash
$ python main.py --mode=train --dataset Both --image_size 256 --c_dim 5 --c2_dim 8 \
                 --sample_dir stargan_both/samples --log_dir stargan_both/logs \
                 --model_save_dir stargan_both/models --result_dir stargan_both/results
```

To train StarGAN on your own dataset, create a folder structure in the same format as [RaFD](https://github.com/yunjey/StarGAN/blob/master/jpg/RaFD.md) and run the command:

```bash
$ python main.py --mode train --dataset RaFD --rafd_crop_size CROP_SIZE --image_size IMG_SIZE \
                 --c_dim LABEL_DIM --rafd_image_dir TRAIN_IMG_DIR \
                 --sample_dir stargan_custom/samples --log_dir stargan_custom/logs \
                 --model_save_dir stargan_custom/models --result_dir stargan_custom/results
```


### 4. Testing

To test StarGAN on CelebA:

```bash
$ python main.py --mode test --dataset CelebA --image_size 128 --c_dim 5 \
                 --sample_dir stargan_celeba/samples --log_dir stargan_celeba/logs \
                 --model_save_dir stargan_celeba/models --result_dir stargan_celeba/results \
                 --selected_attrs Black_Hair Blond_Hair Brown_Hair Male Young
```

To test StarGAN on RaFD:

```bash
$ python main.py --mode test --dataset RaFD --image_size 128 \
                 --c_dim 8 --rafd_image_dir data/RaFD/test \
                 --sample_dir stargan_rafd/samples --log_dir stargan_rafd/logs \
                 --model_save_dir stargan_rafd/models --result_dir stargan_rafd/results
```

To test StarGAN on both CelebA and RaFD:

```bash
$ python main.py --mode test --dataset Both --image_size 256 --c_dim 5 --c2_dim 8 \
                 --sample_dir stargan_both/samples --log_dir stargan_both/logs \
                 --model_save_dir stargan_both/models --result_dir stargan_both/results
```

To test StarGAN on your own dataset:

```bash
$ python main.py --mode test --dataset RaFD --rafd_crop_size CROP_SIZE --image_size IMG_SIZE \
                 --c_dim LABEL_DIM --rafd_image_dir TEST_IMG_DIR \
                 --sample_dir stargan_custom/samples --log_dir stargan_custom/logs \
                 --model_save_dir stargan_custom/models --result_dir stargan_custom/results
```
### 5. Pretrained model
To download a pretrained model checkpoint, run the script below. The pretrained model checkpoint will be downloaded and saved into `./stargan_celeba_256/models` directory.

```bash
$ bash download.sh pretrained-celeba-256x256
```

To translate images using the pretrained model, run the evaluation script below. The translated images will be saved into `./stargan_celeba_256/results` directory.

```bash
$ python main.py --mode test --dataset CelebA --image_size 256 --c_dim 5 \
                 --selected_attrs Black_Hair Blond_Hair Brown_Hair Male Young \
                 --model_save_dir='stargan_celeba_256/models' \
                 --result_dir='stargan_celeba_256/results'
```

