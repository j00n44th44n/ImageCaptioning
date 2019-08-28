Image Captioning (machine translation(21) + transfer learning (8,10) for images)

Transfer learning
given an `some` model without the final layer (classification layer) the output value is saved in a cache file in the hard drive and is used it as the input for another neuronal network

VGG16 Model
input layer -> convolutional blocks 1...5 -> | dense 1..2 -> output layer

to classify images from a new data set we replace this "dense 1..2 -> output layer"
and root the output to a fully connected layer with a dropout layer to prevent overfitting

Encoder - Decoder
machine translation (ex NLP danish to english)

Encoder: (summarize the content of the input)
Embedding layer + 3 gather recurrent unit -> output vector

Recurrent units can't work on text data so they have to be converted in -1 to 1 float values

Decoder: (generate a sequence of words)
Embedding layer + 3 GRU layer + dense layer

Image captioning:
Replace the encoder part of the network for a pre-trained image model (VGG16 model)

input layer -> convolutional blocks 1...5 -> dense 1..2 fully connected -> `dense map`

replace the output layer (|1000| vector).
     _____           _____                          
    |dense| _____\  |dense| 4096 mapped to 512 as the initail state of       |__2__|      /  |_MAP_| the decoder.

Intermidian fully connected layer

Training Process
decoder(Initial_State_512_vector, Sequence_of_Integer_tokens, Same_sequence_left_shifted)
Embeding: integer -> 128 floating point vector
GRU1 output a sequence of vectors of 512 elements each, and used as the input of GRU2

Inference Process
decoder(Initial_State_512_vector, initial_marker_'ssss')
output: should produce a sequence of words captioning the image.

Code...

use coco data set.

 _________________
|                 |        caption 1
|                 | --->     ...
|_________________|        caption n

data set for training, validation, testing...
load pre-trained image model VGG16 using keras

