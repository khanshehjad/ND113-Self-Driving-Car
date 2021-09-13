# ND113-Self-Driving-Car
Deep learning autonomous car built with TensorFlow, Raspberry Pi and Google's EdgeTPU Co-Processor.

### Lane Navigation Model
Based model on NVidia's [End-to-end Self Driving Model](https://arxiv.org/abs/1604.07316) CNN Architecture. It contains about 30 layers in total, not very deep. The input image to the model (bottom of the diagram) is a 66x200 pixel image, which is a pretty low-resolution image. The image is first normalized, then passed through 5 groups of convolutional layers, finally passed through 4 fully connected neural layers and arrived at a single output, which is the model predicted steering angle of the car.

![image](https://user-images.githubusercontent.com/31896767/133016052-aaf9e0a5-6dda-4239-aab9-d4b98166bafe.png)

It contains about 30 layers in total, not a very deep model by today’s standards. The input image to the model (bottom of the diagram) is a 66x200 pixel image, which is a pretty low-resolution image. The image is first normalized, then passed through 5 groups of convolutional layers, finally passed through 4 fully connected neural layers and arrived at a single output, which is the model predicted steering angle of the car.

![image](https://user-images.githubusercontent.com/31896767/133016324-6c1cac0f-5cca-4456-a163-a8cb6d1e3218.png)

This model predicted angle is then compared with the desired steering angle given the video image, the error is fed back into the CNN training process via backpropagation. As seen from the diagram above, this process is repeated in a loop until the errors (aka loss or Mean Squared Error) is low enough, meaning the model has learned how to steer reasonably well. Indeed, this is a pretty typical image recognition training process, except the predicted output is a numerical value (regression) instead of the type of an object (classification).

Note that I have fairly faithfully implemented the Nvidia model architecture, except that I removed the normalization layers, as I would do that outside of the model, added a few dropout layers, to make the model more robust. The loss function I use is Mean Squared Error (MSE) because it is doing regression training. I also used the ELU (Exponential Linear Unit) activation function instead of the familiar ReLU (Rectified Linear Unit) activation function because ELU doesn’t have the “dying RELU” problem when x is negative.
