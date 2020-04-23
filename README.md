# ImageCaptioning

Image Captioning is the union of machine translation and transfer learning for images.

Given an input image our used encoder model (VGG16) will extract 4096 feature vector reduced in a dense map to 512 and used to feed our decoder model.

With the features vector and the correct label tokenized adjust weights in the CNN in order to produce the same answer one time shifted to the left.

‘ssss’ big brown bear sitting ‘eeee’

_____________________________________
  
  `MODEL`

_____________________________________
 

big brown bear sitting ‘eeee’

The idea behind this is the model learn with the given input feature vector and the start marker ‘ssss’ (‘eeee’ is the end marker) it should produce the word right next to the marker.

<feature vector> + ‘ssss’ => big
<feature vector> + ‘ssss’ + ‘big’ => ‘brown’ 
<feature vector> + ‘ssss’ + ‘big’ + ‘brown’ => ‘bear’
<feature vector> + ‘ssss’ + ‘big’ + ‘brown’ + ‘bear’ => ‘sitting’
<feature vector> + ‘ssss’ + ‘big’ + ‘brown’ + ‘bear’ + ‘sitting’ => ‘eeeee’

Then we use the same model structure already trained and extract the feature vectors from the image and give them as input with the token ’ssss’ to get the first word of our label, and so on until the ‘eeee’ token comes up
