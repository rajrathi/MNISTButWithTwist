# MNIST, But with a TWIST!!!

The problem statement is to predict two things with NN, first the MNIST images and second the addition of lables of MNIST with a random integer ranging between 0 and 9.

## Dataset

The dataset consists of four things:
- MNIST images
- labels for MNIST images
- one-hot encoded random integers ranging from 0 to 9
- tensor of size five containing class probabilities for binary represantation of sum of MNIST label and random number, as we can consider there are five classes. For an example, we can consider when sum = 13, it binary representation will be [1, 0, 1, 1, 0], this tensor will be converted into [0.33, 0., 0.33, 0.33, 0.]

> The function to generate the random numbers is __torch.randint(0, 9, len(mnist_data))__ where mnist_data is MNIST train dataset. The random numbers are then one-hot encoded in the size of (60000, 10)

## Training

The batch of MNIST images were first given to the network and they were convolved and flattened  for giving as input to the first fully connected layers as 1600 neurons. 
- Now, we had choice to add our one-hot encoded tensor of size 10 here. But, we didn't combined with 1600 neurons as, Network could have ignored that number because of other 1600 numbers.
- Secondly, we could've introduced the number in the image itself at corner, but while convolving, that number also have been ignored
- So, __I combined those random numbers to second fully connected layer__ which reduced 1600 neurons from first fc layer to only 120 neurons, and adding 10 more scalars would have been significant to network.
- Lastly the output for MNIST label was taken from third FC layer and softmax was used at the end, but the output for additon was taken after reducing third FC layer to forth FC layer and then giving output in five neurons followed by softmax function. __Five neurons were used in the output, as we are considering sum as binary represnation which only require five digits.__





