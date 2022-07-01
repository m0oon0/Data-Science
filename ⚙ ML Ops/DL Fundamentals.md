
## Universality

"Universal function approximation theorem"

Given any continuous function f(x), if a 2-layer neural network has enough hidden units, 
then there's a choice of weights that allow it to closely approximate f(x).

![image](https://user-images.githubusercontent.com/79262676/162991625-b5c8be94-af82-4bad-a3f1-ae2f58e4cdcd.png)

## Learning problems

◾ Supervised learning

-> Get labeled data X and Y

-> Learn function X -> Y

e.g. image/speech recognition, machine translation,

◾ Unsupervised learning

-> Get unlabeled data X

-> Learn the structure of X

e.g. predict next words (RNN) or nearby words (word2vec), predict next pixel (pixelCNN), AutoEncoder, GAN,

![image](https://user-images.githubusercontent.com/79262676/162984019-e9c902e0-914d-46e2-ab8c-62993143a23f.png)

Not given labels : just understanding patterns or relationships of input data.

◾ Reinforcement learning

-> Learn how to take Actions in an Environment, through reward

## Empirical risk minimization & Loss function

Finding best weights that minimize error (=loss).

The whole concept of learning = Optimize loss

◾ Simple Linear Regression
![image](https://user-images.githubusercontent.com/79262676/162985665-c2e2d22f-8db5-4e36-9b25-7da172b00ec1.png)

◾ Neural Network Regression

![image](https://user-images.githubusercontent.com/79262676/162985750-ec20bde5-a15e-4272-84e9-9fcfd9f0d0bd.png)

◾ Goal : find W, b that optimize (minimize) the Loss

◾ might be ...

![image](https://user-images.githubusercontent.com/79262676/162986338-f7bc75b8-b93f-40be-a9e3-76d4d1d97a58.png)

not able to find closed form solutions...

## Gradient Descent

![image](https://user-images.githubusercontent.com/79262676/162986951-ae780068-7a2a-4884-b76c-20f6e360d076.png)

- Update W, through gradients of the Loss function (with regard to W) so that move toward steepest descent

(+) conditioning 

- normalization (batch norm, weight norm, layer norm, ..)

- techniques e.g. Adam

- sampling schemes : stochastic GD (compute each step on just a batch (subset) of data

How to efficiently compute the gradients in Neural Network? ...

## Backpropagation

Gradients are just derivatives : 
Apply chain rule backward, chaining through all of the layers of neural net.

## Architectural considerations

![image](https://user-images.githubusercontent.com/79262676/162990484-bfd7a81a-b26a-4049-ade9-91f4622a7f59.png)

(+) optimization & conditioning

- depth / width of layers

- skip connections

- batch / weight / layer normalization

## Computing NN

All NN computations are just matrix multiplications, thus are easy to parallelize onto GPU.
