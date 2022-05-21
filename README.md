# Emotion-detection-and-caption-generation
The model consists of two architectures, one for emotion detection and another for caption generation.<br>

Emotion detector uses a CNN architecture with a softmax layer at the top for classifiaction on FER2013 dataset.<br>
Caption generator uses a CNN and transformer model. EfficientNet has been used as a feature extractor. We have trained the transformer from stratch(using pretrained word embeddings) instead of using a pretrained transformer model like BERT, GPT, etc.
<br>

<h2> Emotion Detector </h2?
We have used fer2013 dataset to train our emotion detection model.<br>
The model CNN architecture consists of the following types of layers:<br>
	CONV2D layer<br>
	Maxpooling layers<br>
	Batch normalization layer<br>
	Topmost fully connected layers<br>
	Softmax layer for classification<br>
<br>
<h3>Working of emotion detector model </h3>
<br>
•	The model is trained by passing the fer2013 dataset image through the CNN architecture explained before.<br>
•	The conv layers find patterns and maintain locality by finding relations and patterns between the neighbour pixels.<br>
•	The maxpooling layers provide translational invariance.<br>
•	Batch normalization layers help in faster convergence.<br>
•	We have used data augmentation and early stopping to reduce overfitting.<br>
•	The conv layers are flattend into a fully connected network with a softmax activation at the last layer to predict the emotion.<br>
•	The best of 5 accuracy achieved was approx. 60%, whereas the human level accuracy on the dataset is approx. 65%.<br>
<br>
Epochs running can be understood from the below image:
<br>
 ![image](https://user-images.githubusercontent.com/79802235/169638321-d95e9d2f-3907-4d53-b482-ccd3fd92abe2.png)


<h2> Caption Generator </h2>
<br>
We have trained our caption generator on the flickr8k dataset because it contains a large number of images focusing on people and their actions. The model architectures consists of the following:<br>
	A CNN architecture using transfer learning on Efficientnet<br>
	A transformer encoder block<br>
	A transformer decoder block<br>

<h3>Working of caption generator model </h3><br>

	CNN architecture<br>
The CNN architecture is taken from efficientnet using transfer learning.<br>
The last layer of efficientnet has been removed as we don’t need to classify, instead we just need to get an image encoding to pass as an input to the encoder layer of the transformer. Thus, the efficientnet is used as a feature extractor.<br>

	Transformer Encoder block<br>
This encoder block takes the image encoding as the input and applies attention to it before passing it to the decoder block. <br>

	Transformer Decoder block<br>
The five captions per image are passed one by one to the decoder along with the encoder outputs. Masked attention is applied to the sequence inputs to predict the next word.<br>

Epochs running can be understood from the below image:<br>

![image](https://user-images.githubusercontent.com/79802235/169638316-4000429e-4285-44cb-8767-4cd1892a4b78.png)

 <h3> Why using transformers ? </h3><br>

Transformers (Attention is all you need) were introduced in the context of machine translation with the purpose to avoid recursion in order to allow parallel computation (to reduce training time) and also to reduce drops in performance due to long dependencies. The main characteristics are:<br>
•	Non sequential: sentences are processed as a whole rather than word by word.<br>
•	Self Attention: this is the newly introduced 'unit' used to compute similarity scores between words in a sentence.<br>
•	Positional embeddings: another innovation introduced to replace recurrence. The idea is to use fixed or learned weights which encode information related to a specific position of a token in a sentence.<br>
The first point is the main reason why transformer do not suffer from long dependency issues. The original transformers do not rely on past hidden states to capture dependencies with previous words. They instead process a sentence as a whole. That is why there is no risk to lose (or "forget") past information. Moreover, multi-head attention and positional embeddings both provide information about the relationship between different words.<br>


 ![image](https://user-images.githubusercontent.com/79802235/169638304-6a103f0c-079a-4c00-86f2-8dd791c62914.png)



