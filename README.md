# Stochastic_inplace_weight_dropout


In this notebook I implement a variant of an idea I had: weight dropout. Essentially weight dropout is a process in
which a neural network follows a policy consiting in setting a percentage of its weights to zero (when a condition 
is met). This variant, named stochastic inplace weight (SIW) dropout, randomly sets a specified percentage of 
weights, every specified number of epochs to zero. Each time SIW dropout is performed the weights are also scaled 
accordingly. The principle behind SIW dropout is to improve generalization by introducing small and random 
disruptions in the training process to aid the learning alogirithm in finding a better local minima. By hindering
the training process, the network overfits at a slower pace while performance is maitained. It may also be helpful
in improving training if a network is trained with a suboptimal learning rate. 

In January I tested SIW dropout with a simple and small fully connected network using the boston housing dataset.
This testing yielded promising results; SIW dropout made the network train faster and generlize slightly better. 
SIW was later tested on CNNs however it had a detrimental peformance when applied to the convolutional layers. 
Therefore I decided to stick to testing SIW on fully connected layers. I tried SIW dropout on the last FC layers
of VGG-16, but it made more sense to test in transformers since they contain more FC layers. Below I test SIW 
dropout on a bigger network, VIT. Here SIW dropout is applied to every FC layer in the network. The best results 
are achived with a SIW dropout probability of 5% at a rate of 1 time every 3 epochs (curiously this choice of 
parameters also displayed the best results in smaller networks). 

Both files uploaded to this repository contain the notebook where SIW dropout was tested. The graphs below are 
from notebook 2. 

<img width="812" alt="image" src="https://user-images.githubusercontent.com/22745975/165368741-1c1a7d66-efcc-4466-baba-cecdd84571f4.png">

<img width="830" alt="image" src="https://user-images.githubusercontent.com/22745975/165368832-d39a5074-0933-4eb9-bb01-40fb43814167.png">

5% probabilty yielded the best results. To confirm this these tests where repeated 10 times and the average was taken.

<img width="825" alt="image" src="https://user-images.githubusercontent.com/22745975/165369545-e2ed89f0-3cb9-45d0-a950-a9cd4372590a.png">

<img width="834" alt="image" src="https://user-images.githubusercontent.com/22745975/165369584-573d5002-16f7-43b2-a127-98bf170ad674.png">

SIW dropout clearly helped stabilize the validation loss and granted a slight performance increase. 

(Some graphs on notebook 1 have 'SIW' incorrectly label as 'boston')

Antorbus
