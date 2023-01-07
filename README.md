# MNIST, But with a TWIST!!!

The problem statement is to predict two things with NN, first the MNIST images and second the addition of lables of MNIST with a random integer ranging between 0 and 9.

## Dataset

The dataset consists of four things:
- MNIST images
- labels for MNIST images
- one-hot encoded random integers ranging from 0 to 9
- tensor of size five containing class probabilities for binary represantation of sum of MNIST label and random number, as we can consider there are five classes. For an example, we can consider when sum = 13, it binary representation will be [1, 0, 1, 1, 0], this tensor will be converted into [0.33, 0., 0.33, 0.33, 0.]. This tensor will be feed to Cross Entropy Loss function to calculate loss for addition.

> The function to generate the random numbers is __torch.randint(0, 9, len(mnist_data))__ where mnist_data is MNIST train dataset. The random numbers are then one-hot encoded in the size of (60000, 10)

## Training

The batch of MNIST images were first given to the network and they were convolved and flattened  for giving as input to the first fully connected layers as 1600 neurons. 
- Now, we had choice to add our one-hot encoded tensor of size 10 here. But, we didn't combined with 1600 neurons as, Network could have ignored that number because of other 1600 numbers.
- Secondly, we could've introduced the number in the image itself at corner, but while convolving, that number also have been ignored
- So, __I combined those random numbers to second fully connected layer__ which reduced 1600 neurons from first fc layer to only 120 neurons, and adding 10 more scalars to the second FC layer would have been significant to network.
- Lastly the output for MNIST label was taken from third FC layer and softmax was used at the end.
- The output for additon was taken after reducing the third FC layer to the forth FC layer and then giving output in five neurons followed by softmax function. __Five neurons were used in the output, as we are considering sum as binary represnation which only require five digits.__

## Evaluation

There are two outputs, we need to evaluate. One for MNIST images and other for addition of labels and random numbers.

- For MNIST, we equated the argmax of prediction with the labels and calculated the total accuracy.
- Now for addition, we converted the prediction into 1s and 0s similar to binary reprentation by making top _**N**_ values in the prediction into 1s and rest zeros. This tensor is equated with the binary representation of sum. If it results in true, we increase the count by 1 for correct predictions. _(Here N is the number of 1s present in correct binary represenatation of sum)_

For an example, the correct sum is 11, the representation of our sum label is [0.33, 0.33, 0., 0.33, 0.]. This will be converted into [1., 1., 0., 1., 0.]. So, here our N = 3. 
Now our prediction comes out to be [0.27, 0.12, 0.31, 0.2, 0.1]. Now converting the top N values to 1 and others zero [1., 0., 1., 1., 0.]. <br>
Equating the respective tensors from above, the result is false. Therefore we didn't increase the count by 1.

### Results
> Finally, We got accuracy of 99.78% for MNIST images, and 62.64% for addition of lables and random numbers. 

## Loss Function

The loss function used for addition of lables and random numbers is Cross Entropy(CE) function. As it compares the probability distribution of the multiple classes between the actual probabilities and predicted probabilities, it suites most to how I solved this problem. <br> As I converted the sum into binary represntation, therefore we had five classes and we can represent the five classes into probabilities for each class. <br><br>
__The CE function takes input as class probabilities for labels as well as for prediction__, we converted the binary representaion into class probability, where we divided probability equally among digit 1 in binary. And prediction already have class probabilities, we don't need to transform them. 
> Suppose there are four ones and two zeros, we equally assigned four ones to probability of 0.25 and the zeros we kept same.

## Trainig Log
__Below is the short training log:__ <br>
epoch: 0 
<br> 	 MNIST: total loss:  841.63 acc:  66.52 
<br> 	 Addition: total loss:  716.23 acc:  30.84
<br>epoch: 1 
<br> 	 MNIST: total loss:  742.74 acc:  87.79 
<br> 	 Addition: total loss:  706.50 acc:  34.83
<br>epoch: 2 
<br> 	 MNIST: total loss:  714.16 acc:  94.09 
<br> 	 Addition: total loss:  666.46 acc:  43.20
<br>epoch: 3 
<br> 	 MNIST: total loss:  693.29 acc:  98.48 
<br> 	 Addition: total loss:  640.79 acc:  49.05
<br> . . . .
<br>epoch: 16 
<br> 	 MNIST: total loss:  686.50 acc:  99.77 
<br> 	 Addition: total loss:  621.23 acc:  62.18
<br>epoch: 17 
<br> 	 MNIST: total loss:  686.77 acc:  99.72 
<br> 	 Addition: total loss:  620.66 acc:  62.39
<br>epoch: 18 
<br> 	 MNIST: total loss:  686.58 acc:  99.76 
<br> 	 Addition: total loss:  620.01 acc:  62.52
<br>epoch: 19 
<br> 	 MNIST: total loss:  686.44 acc:  99.78 
<br> 	 Addition: total loss:  619.78 acc:  62.64

You can find the complete training log here: [Training Log](trainingLogs.txt)





