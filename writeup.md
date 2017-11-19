## Project: Follow Me

### Network Architecture
The architecture for this network was a fully convolutional network, consisting of two encoder layers and two decoder layers which are connected by a 1x1 convolution layer.  This was same network architecture used in the semantic segmentation lab (lesson 6-8), so this is what I defaulted to for the project network.

![image_1](/network_architecture.jpeg)

The two encoder layers serve the purpose of pulling out features that will help with segmentation of the image, with each layer being useful for characterizing increasingly complex geometry and features.  The 1x1 convolution layer is in place to preserve spacial information.  After the 1x1 convolution layer comes the decoder stage, which uses bilinear upsampling to upsample the image back to its original size.  Skip connections are used during this process to retain information that would have otherwise been lost between the encoder/decoder layers.  In my network I added skip connections to both decoder layers, concatenating the upsampled image with the pre-encoded image.  

### Parameters and Training
The final parameters I picked to achieve the 40% threshold were as follows:

**Learning rate:** 0.007 
**Batch size:** 128
**Number of Epochs:** 30
**Steps per epoch:** 200
**Validation steps:** 50
**Workers:** 2

I arrived at these numbers after a series of model trainings that left me just under the 40% benchmark.  I originally started out with a learning rate of 0.1, 5 epochs, and only 10 steps per epoch.  At this point I was still attempting to run the training on my personal computer, so even this light run took a couple hours, and yielded an IOU close to zero.  Next I bumped up to 10 epochs with 20 steps each, and ran this overnight.  When the model stalled out about halfway through, I knew it was time to head to AWS as suggested in the lessons.  After moving to AWS I was able to increase the batch size, number of epochs, and steps per epoch significantly while also cutting down the training time to a fraction of what it was on my personal computer.  I continued to use the default values for steps per epoch, validation steps, or workers parameters from the original cloned repo.  Therefore I mainly focused my tuning on learning rate and number of epochs.  I found that decreasing my learning rate to 0.01 from 0.1 significantly improved the model, but was still in the 30% score range.  After that I found decreasing the learning rate a little more (from 0.01 to 0.007) while also increasing the number of epochs up to 30 took the model over the 40% threshold.              

### Wrap-up/Future Enhancements
In order to further increase my score I definitely would like to collect more data and play around with the tuning parameters even further.  I certainly don't see my work being done on this project just because I achieved the minimum score!  I also enjoyed learning the AWS interface for this project so performing more training with different network architectures and parameters is something I definitely want to continue doing. As of now, this model and data would not work for following a different object (dog, cat, car, etc).  This would require more data be collected for these particular objects and retraining the model.  This would however be quite an interesting and fun addition to work on down the road as I continue to update my model.    
