### Sequence problems

\- Time Series, Text, Audio, Sequence of images (Video) tasks  
\- one-to-many, many-to-one, many-to-many, ..

Why not use feed forward network?  
Problem 1 : Variable input length  
Problem 2 : Memory scaling  
Problem 3 : overkill (has to learn input from every single position)

### RNNs

Core idea : Stateful computation

Update the hidden state & Compute the output with the hidden state.  
![image](https://user-images.githubusercontent.com/79262676/167640241-2c90379c-0860-49e5-98e8-47522a49450e.png)

Learnable parameter (weight) Whh & Wxh for computing hidden state.

### Encoder-Decoder model

![image](https://user-images.githubusercontent.com/79262676/167641065-323667c0-ada5-4856-80ff-22516efb8131.png)
![image](https://user-images.githubusercontent.com/79262676/167641118-731aba9d-c83f-43ac-8591-4b8729274cd8.png)
![image](https://user-images.githubusercontent.com/79262676/167641200-5902079a-9e3d-489f-8e70-7994de884454.png)

Those three differ in the type of data, but have the same structure of encoder-decoder.  
We can use whatever model we need as the encoder or decoder, based on the type of data.  
In many-output models, y is acting like the output of the decoder model as well as an input of the decoder.  

### Sequence loss function

Sum of cross-entropy loss from all sequence
 
### Sequence input problems

\- All the information in the input sequence is condensed into one hidden state vector.  
\- This becomes a problem as the input sequence gets longer.  

### Vanilla RNN

\- Can't handle more than 10-20 timestamps  
\- Long-term dependencies get lost : Vanishing gradients  

Backpropagation through time  
![image](https://user-images.githubusercontent.com/79262676/167644435-0a1eb3fb-cf2b-4b6f-bb6a-67d4e1558d44.png)
![image](https://user-images.githubusercontent.com/79262676/167644488-7281615d-4a71-4a15-bd7b-c810f3973d1b.png)
![image](https://user-images.githubusercontent.com/79262676/167644620-acf55d8d-21e5-4a32-9500-35f28a955a82.png)

(ReLU RNNs have the opposite problems : Exploding Gradients)  

Goal : Handle long sequences  

### LSTM

Core idea : Introduce a new `cell state` channel  

* Forget gate : decide which parts of old state to forget  
* Input gate : decide how much new input to use when updating the cell state  
* Output gate : compute hidden state.  

\- LSTMs work well for most tasks.  
\- An empirical experiments concludes that GRUs beat LSTMs, so try GRUs when LSTM doesn't work well.  

### Applications for Machine Translation  

How they solved the problem  
1. Used single layer LSTM -> Underfitting  
2. Stacked LSTM layers  -> Works poorly with over 8 layers  
3. Add residual connections  
4. Still, information bottleneck problem between encoder & decoder remains  
5. Attention mechanism (for long term) : Instead of compressing into a single hidden state, give the decoder access to the entire hidden state.   
6. But, LSTMs only consider past informations -> Cannot use future informations.  
7. Bidirectional LSTM (for future information) : Use one LSTM to process the sequence on forward order, the other in backward order.  

![image](https://user-images.githubusercontent.com/79262676/167648726-04208c7c-b1d5-4464-aa67-c80183eb6ce5.png)
 
