# concept - Deep Learning

## Convolutional Neural Network
CONV layer is a set of filters that spatially slide across input volume and output dot product during each step.
    - why: fully connected too many parameters for even a small image, parameter sharing, sparsity of connection
    - convolve: the action of sliding over width and height
    - local connectivity: each filter only look at input volume within the filter window, NOT fully connected
    - filter: matrix of size (f,f,c), f is mostly odd, c is the same as input volume depth (n,n,c)
    - depth: hyperparameter, number of filters, depth column, or fiber
    - stride: Step size when convolve the filter, mostly 1 or 2
    - pooling: reduce size of representation, speeds up computation, more robust features.
        - hyperparameter: (f,f,s) s is step size
        - output: n+2p-f+1 / s,
            - Max Pooling: max(spatial filter)
            - Average Pooling: less common, used to collapse
    - structure: input -> layer 1 (conv1, pool1) -> layer 2(conv2, pool2) -> layer 3(fully connected), layer 4(FC) -> softmax
