# MNIST, But with a TWIST!!!

The problem statement is to predict two things with NN, first the MNIST images and second the addition of lables of MNIST with a random integer ranging between 0 and 9.

## Dataset
The dataset consists of four things:
- MNIST images
- labels for MNIST images
- one-hot encoded random integers ranging from 0 to 9
- tensor of size five containing class probabilities for binary represantation of sum of MNIST label and random number, as we can consider there are five classes. For an example, we can consider when sum = 13, it binary representation will be [1, 0, 1, 1, 0], this tensor will be converted into [0.33, 0., 0.33, 0.33, 0.]

> The function to generate the random numbers is torch.randint(0, 9, len(mnist_data)) where mnist_data is MNIST train dataset. The random numbers are then one-hot encoded in the size of (60000, 10)





