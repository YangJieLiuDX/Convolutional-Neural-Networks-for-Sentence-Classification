# Convolutional-Neural-Networks-for-Sentence-Classification
In this project, we attempt to reproduce and improve the results achieved by Yoon Kim (2014), in [1] with no published code. We implement the proposed models in his paper, which describes sentence classifiers using CNN on top of pre-trained word vectors, Word2Vec. Classification in [1], is performed on multiple datasets, with static and minimally fine-tuned Word2Vec, feeding a single layer CNN. To improve the state-of-the-art, both static and fine-tuned word vectors are used in 2 separate channels to classify sentences[1]. In this work, we simplify Kim’s approach and instead focus only on the use of different kernel sizes with parallel layers. We see that the skill of the model on the unseen test dataset was very impressive, achieving 89%, which is above the skill of the model reported in the 2014 paper. We observed, fine-tuning the pre-trained vectors for specific task improves accuracy over static vectors, and we were able to reach accuracy mentioned in [1] for MR dataset.
<br /> For this project, we reproduce 3 models proposed by Yoon Kim (1-3), and also improve the baseline of Static & Non-static CNN in our model (4):
<br />1. CNN-rand: random initialization of word vector + CNN
<br />2. CNN-static: pre-trained word vectors (word2vec) + CNN
<br />3. CNN-non-static: same as 2, but allow fine-tuning of word vectors for current task 4. CNN-multichannel: parallel multichannel 2,3,4-Gram model + CNN
# Modified Baseline Model
<br />3 Different kernel size, 3-channel: 
<br />3This modification attempts to improve accuracy, by using three input channels for processing 4-grams, 6-grams, and 8-grams of movie review text. Each channel is comprised of the following elements: 1) Input layer which takes length of input sequences as parameter. 2) Embedding layer set to the size of the vocabulary and 100-dimensional real-valued representations using static vectors.3) One-dimensional convolutional layer with 32 filters and a kernel size set to the number of words to read at once. 4) Max Pooling layer to consolidate the output from the convolutional layer. 5) Flatten layer to reduce the three-dimensional output to two dimensional for concatenation. The output from the three channels are concatenated into a single vector and process by a Dense layer and an output layer. Figure 2 shows this model.
Parallel Layers: This multichannel n-gram model is proposed in [1], but simpler since it does not use static and non-static word2vec for each channel. Non-static embedding layer, is input to 3 parallel CNN (not one for each branch as previous model) with 3, 4 and 5 kernel size and output of these parallel layers, then max-pooled and merged. To avoid overfitting of models, a dropout layer with probability of 0.5 is applied once on the concatenation of the max features. figure 3 shows this model

