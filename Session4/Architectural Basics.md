## Architectural Basics

I have put the following points in order of what I think is apt while building network.

-----------------------------------------------------------------
#### How many layers
*These should be added keeping in mind that receptive field = size of object*
#### Receptive Field
*Depends on problem at hand, object detection(receptive field = size of object) or scene detection(receptive field > object size)*
#### SoftMax
*Softmax exaggerates the difference in prediction values, so its usage again depends on problem to solve. Don't use in high accuracy demanding fields - medical diagnosis, self driving cars etc.*

### Above 3 points should be thought about in the very beginning, looking at the images(object size) and also the problem to solve.
-----------------------------------------------------------------


#### 3x3 Convolutions
*generally 3X3 conv. should be used because they can replicate any size conv. effect with much less #params to train.*
#### 1x1 Convolutions
*Used generally when we want to reduce #channels. Doesn't reduce channel size.*
#### Kernels and how do we decide the number of kernels?
*General pattern should be increase kernel size upto a level to learn complex features, then decrease, then again increase upto a level. eg - (32 - 64 - 128 - 256) -> (32 - 64 - 128 - 256). Now this increasing and decresing can be formed by using smaller #kernels eg - (10-16-20) -> (10-16-20) This will depend upon your hardware capacity and also the problem you are trying to solve is complex or easy. eg, greyscale images with few classes is simple, while color images with lot of classes is hard.*
#### MaxPooling
*Max pooling layers will reduce the size of channels by 1/4th or 1/9th depending upon the pool size. So it helps to avoid growing of network too large, as we have to reach the receptive field size till last layer. It is useful to reduce channnel size when there aren't too many details and it is fine to send only loudest feature further.*
#### Position of MaxPooling
*Generally it takes 3-6 conv. layers to extract one level of features(level here means, edges/grad., patterns etc.). So once one level of features are extracted, then it is fine to send only loudest features further, i.e. these one level features. SO generally max pool layer should be used after 3-6 conv. layers depending upon input image size.*
#### Concept of Transition Layers
*Transition layer is a combination of max pool and 1X1 conv layers. So we know that we need to follow incresing and decreasing #kernels pattern in our architecture. So while reducing #kernels, we do by adding a max pool layer followed by 1X1 conv layer.*
#### Position of Transition Layer
*It is again should be placed after 3-6 conv. layers, so that one level of features are passed to further layer.*
#### The distance of MaxPooling from Prediction
*Before atleast 3-4 layers before prediction layer because as we know max pool reduces information which is passed to next layer considerably, we don't want to loose too much of information at the very last of our network.*
#### When do we stop convolutions and go ahead with a larger kernel or some other alternative (which we have not yet covered)
*When channel size is of about 11X11 for input image size of 400X400(and in similar ratio for other image sizes). We do this because at small channel size, conv. is happening unevenly for different pixels.*

### Above 9 points are to make our network architecture correct. These should be thought of next to images and problem understanding. So these points will be used while creating 1st cut of network where we focus on #layers and getting architecture correct.
-----------------------------------------------------------------

#### Image Normalization
*We know that images are set of pixel values ranging from 0-255, now conv. process contain mathematical multiplications and addditions whcih can grow these numerical pixel values too much, so we reduce the scale of each image*
#### When to add validation checks
*Always, we train our network for certain no of epochs, and each epoch may take some amount of time. But it may happen that our best model is at the nth epoch as compared to n+1th epoch. So we should do validation check at every epoch.*
#### How do we know our network is not going well, comparatively, very early
*Compare 2-3 early epochs for different network. It is highly unlikely that one network is showing poor performance in early epochs and later on turns out to be best. So we can compare early our networks through early epochs accuracies*

### Above 3 points are cosmetics ways to quickly check correctness of our networks and also reducing mathematical number explosions
----------------------------------------------------------------------

#### Batch Normalization
*Conv. layers help in extracting different features. But it may happen that same type of feature, eg - edges can be of different intensity in different images, so we need to normalize them. We do it through batch norm., here one at a time, all channels from all layers are extracted for images in each batch and are normalized then.*
#### The distance of Batch Normalization from Prediction
*Batch norm should not be used before prediction layer because, at prediction layer, we want max. seperation between different class features and we don't want to normalize them.*
#### DropOut
*while training some kernels can over learn about a particular feature, in that case overfitting may happen, so dropout randomly switches off, few kernels in each iteration and stop them from over learning. At the same time increasing learning of under utilized kernels. It helps in reducing difference between train and validation accuracy.*
#### When do we introduce DropOut, or when do we know we have some overfitting
*When we see huge difference between train and validation accuracy.*

### Above 4 points are next to be seen where we can improve upon further after we set our architecture right. Here improvement happens because we reduce overfitting and send different intensitiy features equally
----------------------------------------------------------------------

#### Learning Rate
*In gradient decent optimization algorithm, the step size of the gradient change may affect in such a way that we may overstep the global minima and never come to optimal point. So we need to reduce step size as we reach near to optimal point. Reducing learning rate iteratively helps in that.*
#### Number of Epochs and when to increase them
*For higher Validation accuracy requirements, or if the dataset is hard, we may see that training for a shorter time may not give desired results, so we have to train further.*
#### Batch Size, and effects of batch size
*Generally increasing batch size will help model to train better, since it is able to see more varied images at the same time. But we can't always increase batch size too much depending upon our GPU capacity. Ideally all images in our dataset should be sent at once to train the model best, but we send in batches depending upon GPU capacity.*
#### LR schedule and concept behind it
*As explained above, we need to reduce learning rate as we reach global minima. Now when to reduce it and by how much, this we can set up through LR shedulers.*
#### Adam vs SGD
*This makes difference only in very high accuracy requirements. It is generally different algorithms for reaching global minima.*

### Above 5 points are methods to optimize further, when we reach a particular level of accuracy and now is stuck. These should be looked into when we have tried everything else.
--------------------------------------------------------------------

