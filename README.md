# Neural Style Transfer

This is Mingshi Peng & Peimeng Sui's final project for course [Computer Vision - CSCI-GA.2271-001][CVCourse].

We implement the paper [A Neural Algorithm of Artistic Style][Gatys] and   
 [Perceptual Losses for Real-Time Style Transfer and Super-Resolution][Justin] using Torch.

Our project report can be found [here][report].

## Slow Version - Optimization Based Style Transfer
 Based on the paper [A Neural Algorithm of Artistic Style][Gatys]
### Prerequisite
 Make sure to download [VGG-19](https://gist.github.com/ksimonyan/3785162f95cd2d5fee77#file-readme-md) (and the prototxt file) before running the slow-style-tranfer.lua  
 Enable GPU(cuda) support for faster computation.

### Basic Usage:
 Generate an art image using slow version:
```
th slow-style-transfer.lua -cuda \  
   -vgg_path      PATH/TO/VGG19/DIRECTORY \    
   -content_image PATH/TO/CONTENT_IMAGE.jpg \    
   -style_image   PATH/TO/STYLE_IMAGE.jpg \    
   -output_path   PATH/TO/OUTPUT/DIRECTORY
```
  
  
  
## Fast Version - Image Transfermation Network Based Style Transfer
 Based on the paper [Perceptual Losses for Real-Time Style Transfer and Super-Resolution][Justin]
### Prerequisite

 VGG-16 is needed for training new models. Script to download VGG-16 can be found at /models/  
 Enable GPU(cuda) support for faster computation.
 
### Basic Usage
Generate an art image using pretrained models:
> Pretrained models can be downloaded using /trained_model/download_trained_model.sh  

```
th fast-style-transfer.lua -cuda \
   -use_model  PATH/TO/TRAINED_MODEL \ 
   -input_img  PATH/TO/INPUT_IMAGE.jpg \
   -output_img PATH/TO/OUTPUT_IMAGE.jpg 
```

Train an image transformation model:
> Before training, please refer to **Step 1** of [Johnson's GitHub][TrainModel] on how to prepare the dataset and produce the hdf5 file needed for the training

```
th train_model.lua -cuda \ 
   -h5_file    PATH/TO/TRAINING_DATASET \
   -max_train  20000 \
   -content_weight 2.0 -style_weight 5.0 \ 
   -TV_weight  1e-5 \
   -jobid default 
```


[CVCourse]:http://cs.nyu.edu/~fergus/teaching/vision/
[Gatys]:https://arxiv.org/abs/1508.06576
[Justin]:http://cs.stanford.edu/people/jcjohns/eccv16/
[TrainModel]:https://github.com/jcjohnson/fast-neural-style/blob/master/doc/training.md
[report]:http://cs.nyu.edu/~mp4504/Implementation-Two-Approaches.pdf



