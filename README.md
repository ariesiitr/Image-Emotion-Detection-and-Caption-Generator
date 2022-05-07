# Emotion-detection-and-caption-generation
The model consists of two architectures, one for emotion detection and another for caption generation.

Emotion detector uses a CNN architecture with a softmax layer at the top for classifiaction on FER2013 dataset

Caption generator uses a CNN and transformer model. EfficientNet has been used as a feature extractor. We have trained the transformer from stratch(using pretrained word 
embeddings) instead of using a pretrained transformer model like BERT, GPT, etc.
