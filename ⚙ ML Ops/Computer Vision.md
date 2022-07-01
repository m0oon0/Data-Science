CNNs and Computer Vision applications. 

Convolution
---

📍 Why not FC for images?

- Flattening image and fully connecting every node : Too many parameters.
- Only few regions are important in telling what is in the image. 
- FC cannot understand the image as the same, if slight translation is made.
- Translation invariance is what we need for computer vision task : for we augment the data by image translation.

📍 How Convolution filter acts

📍 What can a convolution filter do?

We can produce something by the filter.  
e.g. Cascade filter can detect the eyes, nose, lips of a face.  
Instead of hard-coding the weights, we can make the neural net learn them by training.

📍 Methods in doing convolution

- Padding
Add values (usually 0) to the borders of the image
: Solves the problem of filters running out of image.
: Used to make the size of the output same as the input.

- Striding
Jump across some location : Subsample the image.

Shape
---
📍 Multiple channels

e.g. RGB image with 3 channels

input data with shape CHANNEL_NUM x W x H  
convolutional filter with shape FILTER_NUM x CHANNEL_NUM x f x f  
-> Generates output with shape FILTER_NUM x W' x H'

We can then stack multiple layers with multiple filters.

📍 Shape
![image](https://user-images.githubusercontent.com/79262676/166441581-b6336bca-ebc1-4c6d-90ee-9afeeff49b6e.png)

- Selecting the size of filters : 
Empirical results | Intuition | Experiment | ...

📍 Matrix
![image](https://user-images.githubusercontent.com/79262676/166442910-5c2959d6-27d6-42c6-ad8e-4687f194a146.png)

Other operations
---

📍 Increasing the receptive field

- Stacking convolutions increases the receptive field.
- Tend to perform better than a single large filter.

- Dilated filter
-![image](https://user-images.githubusercontent.com/79262676/166443808-d271a9c4-693e-4272-9e2d-79ec07ea3391.png)


📍 Decreasing the size of tensor

- Pooling
Subsample the image by averaging or taking max of region.
-> Recently fallen out of favor...

Convnet architectures
---

ILSVRC (ImageNet Large Scale Visual Recognition Challenge) yields SOTA models for CV.

📍 LeNet-like architectures

![image](https://user-images.githubusercontent.com/79262676/166444480-77c5eb8f-d4ba-4b97-b2ce-d5e8cc4e35ef.png)

: Baseline architecture for CV tasks.

📍 AlexNet
![image](https://user-images.githubusercontent.com/79262676/166445789-68ed293c-773d-4567-89ed-2f7c2187091d.png)

📍 VGG  
Channel dimension increases with each layer.

📍 GoogLeNet 
- As deep as VGG, but has only 3% of the parameters!  
- No fully-connected layers  
- Stack of Inception Modules.
![image](https://user-images.githubusercontent.com/79262676/166447531-b84986c8-91c3-4afa-8a90-12ea60a8da0d.png)

Instead of picking one, compute through all of them, and concatenate the results.  
Follows hypothesis that cross-channel correlations and spatial correlations are decoupled and can be mapped separately.  

📍 ResNet
- Problem : Deep models should perform better than shallow network, but don't due to vanishing gradient.  
-> Solution : SImply skip layers such that if the gradient vanishes, no harm is done.

![image](https://user-images.githubusercontent.com/79262676/166448241-f5e7a4ec-bf81-40b1-a9ee-af149c44f73b.png)

- Increase number of filters with depth  
✔ Instead of max-pooling, down-sample spatially using strides!

- Variants of ResNet  
DenseNet ; Add more skip connections

📍 SENet

![image](https://user-images.githubusercontent.com/79262676/166449091-fea78458-bc37-4003-be22-571d692db296.png)

Add a module of global pooling & FC layer to adaptively reweight feature output maps.  
The network choose what to use : Act like attention mechanism...

📍 SqueezeNet  

AlexNet level accuracy with 50x fewer parameters & < 0.5MB model,  
through constant 1x1 bottlenecking (= squeeze)

Comparison
![image](https://user-images.githubusercontent.com/79262676/166449413-32ec9254-a94d-488c-9b4e-0cbff8311aaa.png)

Some ResNets, or Inception-v4 (Inception+ResNet) are in the sweet spot of accuracy to operations/memory.

Issues
---
- Fast training with large batch & multiple GPUs.
- 

Computer Vision Tasks
---

Other than classification task : Localization, Detection, Segmentation, ...

![image](https://user-images.githubusercontent.com/79262676/166450026-214ec1d5-6f48-41c7-b4dc-e6fcf97a236f.png)

📍 Localization

Simply predict the `bounding box (x1, y1, x2, y2)` as well as the class, using the same network.

📍 Detection

Localization does not scale when there are multiple objects.

-> Slide a classifier over the image. 
: Very computationally expensive...

Overfeat, YOLO, SSD
---

![image](https://user-images.githubusercontent.com/79262676/166450813-31d5f26b-da0d-4145-b4a0-65d3e08d8f67.png)

Count votes and unify.
When bounding boxes overlap, only the one with the highest score should remain.

- Predict the presence of an object center point, and several acchor boxes.  
- Predict for each anchor boxes and NMS prediction.  

Scaled -> YOLO & SSD(Single Shot Detector)

Region Proposal Methods
---

Not looking every place in an image ; Look only at ROI (Region Of Interest)  
How to find ROI?  

📍 R-CNN
Region Proposal (slow external method : non- deep learning method) and apply AlexNet in ROI  

📍 Faster R-CNN
- Insert RPN (Region Proposal Network)
- Everything is in-network -> fast

📍 Mask R-CNN
- Also go through an instance segmentation module.

Advanced tasks
---

📍 3D shape inference  

Given a 2D image, detect objects and predict their 3D meshes.
Mesh R-CNN
![image](https://user-images.githubusercontent.com/79262676/166453983-c6e70b2d-0250-409d-a365-0d1d2cd52769.png)

Dataset `shapenet`

📍 Face landmark recognition
Dataset `Annotated Facial Landmarks`

📍 Pose estimation
Detect joint...
 
