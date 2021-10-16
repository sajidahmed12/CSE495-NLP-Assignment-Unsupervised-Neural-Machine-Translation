# Neural-Machine-Translation-v Bangla-To English

This is the sequential Encoder-Decoder implementation of Neural Machine Translation using Keras-Tensorflow. This model translates the input Bangla sentence into the corresponding English sentence and vice verca with a **Bleu Score: 0.409124** on the test set.

**Encoder** - Represents the input text corpus (Bangla text) in the form of embedding vectors and trains the model.

**Decoder** - Translates and predicts the input embedding vectors into one-hot vectors representing English words in the dictionary.

![Model](https://github.com/vibhor98/Neural-Machine-Translation-using-Keras/blob/master/images/model.png)

### Code Requirements
You can install Conda that resolves all the required dependencies for Machine Learning.

Run: `pip install requirements.txt`

### Dataset
We're using dataset containing pairs of English - Bangla sentences and can be downloaded from [here](http://www.manythings.org/anki/).
* This dataset is present in `data/ben.txt` file containing 52,820 pairs of English to Bangla phrases.

### Preprocessing the dataset
* To preprocess the dataset, run `pre_process.py` to clean the data and then run `prepare_dataset.py` to break it into smaller training and testing dataset.
* After running the above scripts, you'll get `english-bangla-both.pkl`, `english-bangla-train.pkl` and `english-bangla-test.pkl` datasets for training and testing purposes.

The preprocessing of the data involves:
* Removing punctuation marks from the data.
* Shuffling the sentences as sentences were previously sorted in the increasing order of their length.

### Training the Encoder-Decoder LSTM model
Run `model.py` to train the model. After successful training, the model will be saved as `model.h5` in your current directory.
* This model uses **Encoder-Decoder LSTMs** for NMT. In this architecture, the input sequence is encoded by the front-end model called encoder then, decoded by backend model called decoder.
* It uses Adam Optimizer to train the model using Stochastic Gradient Descent and minimizes the categorical loss function.

### Evaluating the model
Run `evaluate_model.py` to evaluate the accuracy of the model on both train and test dataset.
* It loads the best saved `model.h5` model.
* The model performs pretty well on train set and have been generalized to perform well on test set.
* After prediction, we calculate Bleu scores for the predicted sentences to check how well the model generalizes.

### Calculating the Bleu scores
**BLEU (bilingual evaluation understudy)** is an algorithm for comparing predicted machine translated text with the reference string given by the human. A high BLEU score means the predicted translated sentence is pretty close to the reference string. More information can be found [here](https://en.wikipedia.org/wiki/BLEU). Below are the BLEU scores for both the training set and the testing set along with the predicted and target English sentence corresponding to the given Bangla source sentence.

### References:
* [Neural Machine Translation by jointly learning to Align and Translate](https://arxiv.org/pdf/1409.0473v7.pdf)
* [How to develop a Neural Machine Translation System from scratch](https://machinelearningmastery.com/develop-neural-machine-translation-system-keras/)


##  1. Names and IDs
* Zahin Akram- 1610618042
* Sajid Ahmed- 1610364042
* Arifuzzaman Arman- 1610551042
* Md Rakib Imtiaz- 1610294642

## 2. Contribution Per member:

* All 4 members of the group worked together in understanding the paper 
through by separate and then reading the paper together. All members together began
the training of word embedding through MUSE. It was Sajid and Zahin who looked at the 
code deeply and worked in editing the necessary portion of what was required. Sajid
later ran the model and generated the mapping that was later shown to Sir.

* Sajid looked at the models that were to be used for training once the first part was over.
The decision of the model was decided by Zahin and Sajid together as they were primarily in charge
of the assignment. Once the decision of model was made, further adjustments were made together.
Sajid ran the models necessary in his PC. The dataset was also provided by Sajid.
Sajid oversaw the training in his PC. Zahin and Sajid made final adjustments.

## 3. Notes:

* A lot of issue was the specifications of available systems. The embeddings for the English
vocabulary was extremely large and had to be redone using fewer words. We wrote some code for 
specific amount of vocabulary however even that was not working. We tested that code on some other
files and they worked fine. The problem was that the file was too large that it couldn't be opened.
We had to edit the original final to address the memory error.

* The words chosen were based on frequency. However, most frequent English and Bangla words are different. 
There was also the Unicode error that took a while to solve. It was later solved by the Temporary
use of an UNIX system but it had low specifications and wasn't available for extensive use. 
We had a lot of problems in training and evaluating training as each training took very long and
not the same vector file could be used for every model. We also had infrequent type error issues
as well as environmental issues when running multiple models.

* The work would have been better if we had unrestrained access to a powerful system for an extensive
period of 2 weeks so we could test all our models with varying combinations.


#### Please download the trained_model.pt file from the foloowing link https://drive.google.com/file/d/17-RFIitkcnphSQZ_CkxN_203laTO8lVH/view?usp=sharing
#### -----English To Bangla Translation-----

* python3 translate.py -s data/eng_test.txt -sl e -t out_ben.txt

#### -----Bangla To English Translation-----

* python3 translate.py -s data/ben_test.txt -sl b -t out_eng.txt

also can be run throuth demo.ipynb Directly From Google.collab

## Download the Vectors from these Fast Text links 
https://fasttext.cc/docs/en/crawl-vectors.html
vectors-bn.txt  #link: https://dl.fbaipublicfiles.com/fasttext/vectors-crawl/cc.bn.300.vec.gz

vectors-en.txt  #Link : https://dl.fbaipublicfiles.com/fasttext/vectors-crawl/cc.en.300.vec.gz


and place then in ./data/vec/vectors-{bn.en}.txt
