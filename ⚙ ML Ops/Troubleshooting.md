### Why is Deep Learning troubleshooting hard?

1. Hard to tell that you actually have a bug to begin with
2. Lots of possible sources for the degreadation in performance : Data, Model, Infrastructure..
3. Results can be sensitive to small changes in hyperparameters and dataset makeup

 Poor model performance due to...
 - Implementation bugs : Most DL bugs are invisible
 - Models are sensitive to hyperparameters (learning rate varies a lot by hyperparameters)
 - Data-Model fit
 - Data construction issues : Constructing good datasets is hard  
  -Not enough data  
  -Class imbalances  
  -Noisy labels  
  -Train/Test from different distributions  
 
 ### Strategy for troubleshooting Neural Networks
 
 Key mindset ; Pessimism  
 
 ![image](https://user-images.githubusercontent.com/79262676/174813993-ef89ff1e-438d-45b0-9b2b-f2ff147c7555.png)

### 1. Start simple

1. Choose a simple architecture  
`Images`  
Start with LeNet-like architecture & Consider using ResNet later    
`Sequences`  
Transformer model or WaveNet-like model  
`Multiple input modalities`  
Map each into a lower dimension space - Concatenate - Pass through FC layers  
Or else...  


2. Use sensible defaults  
`Optimizer` Adam optimizer with learning rate 3e-4  
`Activations` Relu for FC and conv models, tanh for LSTMs  
`Regularization & Data normalization` Start with none (Those are very very common source of bugs!)  

3. Normalize scale of input data  
`Images` Scale values to [0,1] or [-0.5, 0.5] (e.g. By dividing by 255)  

4. Simplify the problem  
Start with small training set : Create a simpler synthetic training set  

### 2. Implement & Debug

#### 5 most common DL bugs
![image](https://user-images.githubusercontent.com/79262676/174818600-7f3b64f9-ad1c-4532-858c-dd1c963fdbdb.png)

#### Get the model to run
Step through in debugger & watch for shape, casting, OOM errors

- Start with lightweight implementation
- Use off-the-shelf components (e.g. `keras` tf.layers.dense instead of tf.nn.relu(tf.matmul(W,x)))

1. Shape mismatch & Casting issue (Step through model creation & inference in a debugger)  
Tools  
`Pytorch` ipdb  
`tensorflow` trickier tfdb  

2. Out Of Memory (Scale back one-by-one)

#### Overfit a single batch
Look for corrupted data, over-regularization, errors

1. Error goes up 
2. Error explodes
3. Error oscillates
4. Error plateaus

#### Compare with known results
Iterate until model performs up to expectations

### 3. Evaluation

#### Handling distribution shift  

Use 2 validation sets : one sampled from training distribution & one from test distribution  
`Train-val error` & `Test-val error` Proxy for how much distribution shift is hurting the model performance  

Test error = irreducible error + bias + variance + distribution shift + validation overfitting  

![image](https://user-images.githubusercontent.com/79262676/174823315-d62312ce-c6b3-4b38-bc83-5df241e9af72.png)

### 4. Improve model & data

#### Address under-fitting (reducing bias)

- Make the model bigger (add layers / more units)
- Reduce regularization
- Choose different architecture (closer to SOTA model)
- Tune learning rate & hyperparameters

![image](https://user-images.githubusercontent.com/79262676/174825314-6709f075-af92-4c84-8447-094cc53aeeeb.png)

Now, deal with overfitting

#### Address over-fitting (reducing variance)

![image](https://user-images.githubusercontent.com/79262676/174826027-673f85be-306a-45c9-9947-c7c90148ebd7.png)

#### Address distribution shift

- Analyze test-val set errors & coolect or synthesize more training data to compensate  
- Apply domain adaptation techniques to train & test distributions

e.g. 
![image](https://user-images.githubusercontent.com/79262676/174827028-356ac3a3-09f1-4ad3-abf9-393f30fbcd97.png)
![image](https://user-images.githubusercontent.com/79262676/174827305-12e7ccda-f9bd-4111-8468-fa8a9528c1bb.png)

#### Domain adaptation

Techniques to train on source distribution and generalize to another target using only unlabeled data ot limited labeled data.  
- Correlation Alignment
- Domain confusion
- cycleGAN

#### Re-balance datasets

- If val looks significantly better than test, model overfits to the val set.  
- Due to small val sets / Lots of hyperparameter tuning  
- Recollect validation data or resample
 
