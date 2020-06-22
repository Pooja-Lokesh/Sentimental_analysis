# Sentimental analysis using GRU , Bidirectional LSTM and Multiple Bidirectional LSTMs

## Steps followed :

- Tokenize the text to generate numbers for the words. Optionally set the max number of words to tokenize. The out of vocabulary (OOV) token represents words that are not in the index.
- The numbers in the word index are not ordered, therefore, need to generate sequences for the sentences.
- Adjust the sequences to all be the same length, either by padding them with zeros and/or truncating them.

## Why embeddings:
- Represent words as semantically-meaningful dense real-valued vectors.
- This overcomes many of the problems that simple one-hot vector encodings have.
- Most importantly, embeddings boost generalisation and performance for pretty much any NLP problem, especially if you don’t have a lot of training data.


## Simple RNN : 
RNN have sequential memory 
sequential memory makes it easy for our brain to recognize patterns 
add a loop to aneural netwrok which can pass information forward 
this information is a hidden state which is a representation of previous inputs 
it takes one word at a time, produces the output, then for the next round takes ini the next word till it reaches the end of the inputs
RNN has a problem with retaining the informtaion from the earlier layers 
There is something known as vanishing gradient 
this happens because the nodes in a layer compute the gradient wrt the gradient in the layer before, so if the gradient in smaller before, 
then the gradient will be even more smaller
the gradients decrease exponentially 
due to this the earlier layers barely learn anything 
used tanh cativation function which squishe svakues form -1 to 1

This is why we need LSTMs and GRU 
they are capable of learning long term dependencies called gates 
these gates decide whoch ingormtaion to add or remove from hidden state


LSTM : 
same mechanism as RNN 
cell state is the meedium through which information flows in the network
    it is a memory of a network 
gates decide to keep ot froget a particukar informationa s we progress sequentially ina  RNN
This uses sigmoid activation function , it squishes values from 0 to 1
forget gate,input gate,output gate

teh forget gate decides which informstion to passs on and whihc information to forget 
    the input and the previous hidden state is passed to sigmoid function 
    the closer to 0 means forget and closer to 1 means keep
the input gate 
    the hidden state and input is passed through the sigmoid 
    this decides whoch values need to be updated 
    0 means important 1 means not 
    pass the hidden state an dthe input through the tanh function
    the tan output and the sigmoid output are multiplied
    the sigmoid function decides which information to keep from the tan output
calcculating cell state :
    the cell state is multiplied by the forget vector 
    polarized addition is performed on the cell state and the input gate 
    this gives us new cell state 
output gate 
    this decides which should be the new hidden state 
    the previous hidden state and the input is passed to the sigmoid function 
    the new cell state is passed through the tanh function 
    the output from the sigmoid function and the tanh function are multiplied 
    new hidden state is generated 
these new cell and hidden states are passed to the next step 


GRU :

update gate :
    The update gate helps the model to determine how much of the past information (from previous time steps)
    needs to be passed along to the future.
reset gate :
     It determines how much of the past knowledge to forget. 
less tensor operations 
