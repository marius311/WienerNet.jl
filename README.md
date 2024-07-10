This is a proof-of-concept implementation of the WienerNet architecture (https://arxiv.org/abs/1905.05846) 
in Julia, using Flux/Zygote. It is no longer under development. 

WienerNet takes unfiltered maps of the CMB (either intensity or polarization) and a 2D mask as its inputs, 
and outputs a Wiener filtered version of the input map. The loss function guaruantees mathematically that 
the WienerNet output will approach the exact Wiener filtered input map, without (once training is complete)
suffering the performance penalty of traditional matrix inversion methods such as conjugate gradient. 

The main improvement of this code over the original Keras implementation is increased modularity. Because 
the WienerNet architecture is based on nested layers where each layer halves the dimensions of the input 
map and mask images (up to padding), I implemented a single module called WienerNetBaseBlock which takes 
either nothing (for the deepest layer) or another instance of itself as an input argument and can thus be 
stacked recursively. Finally, a single instance of WienerNetIO serves as the input/output layer. 
