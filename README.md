# Stochastic_inplace_weight_dropout


In this notebook I implement a variant of an idea I had: weight dropout. Essentially weight dropout is a process in
which a neural network follows a policy consisting in setting a percentage of its weights to zero (when a condition 
is met). This variant, named stochastic inplace weight (SIW) dropout, randomly sets a specified percentage of 
weights, every specified number of epochs to zero. Each time SIW dropout is performed the weights are also scaled 
accordingly. The goal behind SIW dropout is to improve generalization by introducing small and random 
disruptions in the training process to aid the learning algorithm in finding a better local minima. By hindering
the training process, the network overfits at a slower pace while performance is maintained. It may also be helpful
in improving training if a network is trained with a suboptimal learning rate (this is inferred because the learning 
rate was not tuned and results show performace increase with SIW, but further research is needed). 

In January 2022 I tested SIW dropout with a simple and small fully connected network using the boston housing dataset.
This testing yielded promising results; SIW dropout made the network train faster and generalize slightly better. 
SIW was later tested on CNNs however it had a detrimental peformance when applied to the convolutional layers. 
Therefore I decided to stick to testing SIW on fully connected layers. I tried SIW dropout on the last FC layers
of VGG-16, but it made more sense to test in transformers since they contain more FC layers. Below I test SIW 
dropout on a bigger network, ViT. Here SIW dropout is applied to every FC layer in the network. ViT was trained and 
tested on CIFAR-10. The best results are achived with a SIW dropout probability of 5% at a rate of 1 time every 3 
epochs (curiously this choice of parameters also displayed the best results in smaller networks). 

Both files uploaded to this repository contain the notebook where SIW dropout was tested. The graphs below are 
from notebook 2, it shows the results of networks (3 were trained and the average of the results was taken) 
trained with diffrent SIW dropout rates and constant probability of 5%. 


Epochs on the x-axis, validation loss on y-axis.
<img width="812" alt="image" src="https://user-images.githubusercontent.com/22745975/165368741-1c1a7d66-efcc-4466-baba-cecdd84571f4.png">

Epochs on the x-axis, validation accuracy on y-axis.
<img width="830" alt="image" src="https://user-images.githubusercontent.com/22745975/165368832-d39a5074-0933-4eb9-bb01-40fb43814167.png">


5% probabilty every 3 epochs yielded the best results. To confirm this, 20 models (10 with and 10 without SIW 
dropout) were trained and the average was taken. Results are shown below.

Epochs on the x-axis, validation loss on y-axis.
<img width="825" alt="image" src="https://user-images.githubusercontent.com/22745975/165369545-e2ed89f0-3cb9-45d0-a950-a9cd4372590a.png">

Epochs on the x-axis, validation accuracy on y-axis.
<img width="834" alt="image" src="https://user-images.githubusercontent.com/22745975/165369584-573d5002-16f7-43b2-a127-98bf170ad674.png">


SIW dropout clearly helped stabilize the validation loss and granted a slight performance increase. 

SIW dropout shows promising results that make it worth investigating more. 
Next steps:
- Apply SIW dropout at a per-batch rate
- Try with networks that are not pretrained 
- Other datasets or network architectures 
- Use in a fully optimized network (with optimal learning rate, batch size, etc...) 
- Try with different optimizers

(Some graphs on notebook 1 have 'SIW' incorrectly label as 'boston', since originally SIW dropout was named 
boston droput)

Antorbus
