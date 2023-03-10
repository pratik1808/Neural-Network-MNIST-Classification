# Neural-Network-MNIST-Classification

## Overview
This website and Python Notebook demonstrates output of a basic Convolutional neural network, consisting of multiple Convolution and Maxpooling layers, followed by a fully connected layer and a softmax layer which gives out 10 probabilities, one for each digit(0-9). 
This model gives a test set accuracy of 99.36%.

## Introduction:

The MNIST dataset is a large database of handwritten digits that is commonly used for training image processing systems. It contains 60,000 training images and 10,000 testing images. Below is a snapshot of some sample images from MNIST dataset.
<p align="center">
  <img width="576" alt="Screenshot 2023-02-19 at 7 39 48 PM" src="https://user-images.githubusercontent.com/101216624/219990319-b6f34043-eda1-4f8e-bbd0-924604546785.png">
</p>


The MNIST dataset is a large database of handwritten digits that is commonly used for training image processing systems. It contains 60,000 training images and 10,000 testing images. Below is a snapshot of some sample images from MNIST dataset.

Our approach to build the neural network for this classifiction problem was to use convolutional neural networks (CNN). A Convolutional Neural Network is a Deep Learning algorithm that can take in an input image, assign importance (learnable weights and biases) to various aspects/objects in the image, and be able to differentiate one from the other. The pre-processing required in a CNN is much lower as compared to other classification algorithms. While in primitive methods filters are hand-engineered, with enough training, CNNs have the ability to learn these filters/characteristics. The figure below shows an example of a CNN model.

The architecture of a CNN is analogous to that of the connectivity pattern of Neurons in the Human Brain and was inspired by the organization of the Visual Cortex. Individual neurons respond to stimuli only in a restricted region of the visual field known as the Receptive Field. A collection of such fields overlap to cover the entire visual area.

<p align="center">
  <img width="697" alt="Screenshot 2023-02-19 at 7 39 57 PM" src="https://user-images.githubusercontent.com/101216624/219990507-f5166911-e41b-4815-beac-cd5395f38a67.png">
</p>
## Method

To train our CNN, we have used 60000 training images which are 28 by 28 pixels each. Each of these image pixels are normalized to have a value between 0 to 1. The benefit of normalizing the input data is that it avoids large gradient values that could make the training process difficult.

All these images are then reshaped in such a way that can be used as an input to the CNN. 60000 images of 28 by 28 pixels each is transformed to a tensor(n dimensional array) of dimensions(60000,28,28,1) and same is the case for 10000 test images(10000,28,28,1)
We then defined the convolutional neural network as a network of Convolutional layers, Maxpooling layers and Dense layers. This is defined explained in detail in the below image:


<p align="center">
  <img width="591" alt="Screenshot 2023-02-19 at 7 40 28 PM" src="https://user-images.githubusercontent.com/101216624/219990609-0003654d-0f64-4341-afe5-0a693d34e86c.png">
</p>

After a series of convolutional, nonlinear, and pooling layers, it is necessary to attach a fully connected layer. This layer takes the output information from convolutional networks. Attaching a fully connected layer to the end of the network results in an N-dimensional vector, where N is the number of classes from which the model selects the desired class. In our case, as you can see, N equals 10 because there are 10 different classes (0 to 9) to predict the class of the input image.

We then trained the CNN by splitting the training dataset into training and validation set, consisting of 20% of the training set. All the parameters (453,908) were adjusted in such a way to minimize the training loss and validation loss as well. We also used regularization in the dense layers to prevent overfitting, resulting in better results on unknown data, i.e. test set.

## Results
This model gives an accuracy of 99.18% on the validation set and an accuracy of 99.36% on the test dataset. We then used this model to be trained on the whole training set and check it's accuracy on the test dataset. This led to overfitting on the training dataset as there was no check on the validation loss and we got an accuracy of 98.53% on the test set when we used the whole training dataset for training. This led to the nuances in the training set being captured well but not so well in the test set. We can achieve higher accuracy on the test set by using a different combination of the convolution and maxpooling layers but even then achieving an 100% accuracy would not be possible on an unknown dataset because there are possible chances of overfitting and misclassification.

In the predictor used for this website we have used the model which was trained along with a validation set, giving us 99.36% accuracy. Below are some of the results from the predictions generated by our model from the test set:


<p align="center">
  <img width="803" alt="Screenshot 2023-02-19 at 7 40 36 PM" src="https://user-images.githubusercontent.com/101216624/219990628-533cd868-4f17-4665-b7c5-55b41912968b.png">
</p>

## What worked well:

As you can see, the above images were predicted correctly, one possible reason of this would be the images being crisp at edges and do not have any different pattern/manuscript and are easy to predict for the human eye as well. These patterns were present in majority in the training set as is the case in any real world scenario, and the network was able to capture the patterns of all 9 images pretty accurately and hence, giving us an accuracy of 99.36%, with only 64 misclassifications from 10000 test images.

There were only 64 misclassifications from the 10000 training examples out of which the distribution of misclassifications is defined below:


<p align="center">
  <img width="304" alt="Screenshot 2023-02-19 at 7 40 42 PM" src="https://user-images.githubusercontent.com/101216624/219990659-cf5c9161-306f-42ba-b696-30a8fe257388.png">
</p>

Most misclassified instances are of the digits 9 and 6. Here???s a look at the images which were misclassified:

## What didn't work well:

It can be clearly seen that the prediction generated by the model is pretty much because of these specific inputs being on the borderline of interpretation between the two numbers, and which could be easily mistaken by the human eye as well. For example, in the first image above, the actual label for the image is 5 but the way in which it is written, incorporating a slightly cursive font, it can easily be misclassified by humans as well as a 6 instead of 5. These images also lack crisp boundaries and are having thick font and mis-interpretable manuscript. Training for more epochs, using a different convolutional layer combination can possibly overcome this to a certain extent but still there are genuine cases of misclassifications as seen above in the case of actual 6 being predicted as a 5, wherein it does not look that much like a 5. Unless these examples are included in the training set, we will not be able to capture their patterns and predict a 6 but using these in the training set might possibly hamper by having overfitting effects.

## Conclusion

With the above Convolutional Neural Network trained on the MNIST dataset, we have achieved an accuracy of 99.36% have built a neural network with 453,908 parameters and are getting only 64 misclassifications on the test dataset. This accuracy can be improved further with more convolutional and maxpooling layers but it is not possible to get an 100% accuracy on the test set, unless we use all the 70000 images to train this neural network. Which is usually not the case with real life scenarios as we do not know what we will encounter during the test phase during the training phase of the model.

This project has given us a very valuable understanding of how CNN's work and we will be looking forward to apply its learnings to more complex and real life business problems to improve business performances.
