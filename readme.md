1. Names and IDs
Zahin Akram- 1610618042
Sajid Ahmed- 1610364042
Arifuzzaman Arman- 1610551042
Md Rakib Imtiaz- 1610294642

2. Contribution Per member:

All 4 members of the group worked together in understanding the paper 
through by separate and then reading the paper together. All members together began
the training of word embedding through MUSE. It was Sajid and Zahin who looked at the 
code deeply and worked in editing the necessary portion of what was required. Sajid
later ran the model and generated the mapping that was later shown to Sir.

Sajid looked at the models that were to be used for training once the first part was over.
The decision of the model was decided by Zahin and Sajid together as they were primarily in charge
of the assignment. Once the decision of model was made, further adjustments were made together.
Sajid ran the models necessary in his PC. The dataset was also provided by Sajid.
Sajid oversaw the training in his PC. Zahin and Sajid made final adjustments.

3. Notes:

A lot of issue was the specifications of available systems. The embeddings for the English
vocabulary was extremely large and had to be redone using fewer words. We wrote some code for 
specific amount of vocabulary however even that was not working. We tested that code on some other
files and they worked fine. The problem was that the file was too large that it couldn't be opened.
We had to edit the original final to address the memory error.

The words chosen were based on frequency. However, most frequent English and Bangla words are different. 
There was also the Unicode error that took a while to solve. It was later solved by the Temporary
use of an UNIX system but it had low specifications and wasn't available for extensive use. 
We had a lot of problems in training and evaluating training as each training took very long and
not the same vector file could be used for every model. We also had infrequent type error issues
as well as environmental issues when running multiple models.

The work would have been better if we had unrestrained access to a powerful system for an extensive
period of 2 weeks so we could test all our models with varying combinations.

4. Requirements: 
				python>=3.5.0
				numpy>=1.14.0
				jupyter==1.0.0
				gensim==3.2.0
				tqdm==4.19.5
				torch==0.3.0
Please download the trained_model.pt file from the foloowing link https://drive.google.com/file/d/17-RFIitkcnphSQZ_CkxN_203laTO8lVH/view?usp=sharing
## -----English To Bangla Translation-----

python3 translate.py -s data/eng_test.txt -sl e -t out_ben.txt

-----Bangla To English Translation-----

python3 translate.py -s data/ben_test.txt -sl b -t out_eng.txt

also can be run throuth demo.ipynb Directly From Google.collab
Requirements: 
			python>=3.5.0
			numpy>=1.14.0
			jupyter==1.0.0
			gensim==3.2.0
			tqdm==4.19.5
			torch==0.3.0

## Download the Vectors from these Fast Text links 
https://fasttext.cc/docs/en/crawl-vectors.html
vectors-bn.txt  #link: https://dl.fbaipublicfiles.com/fasttext/vectors-crawl/cc.bn.300.vec.gz

vectors-en.txt  #Link : https://dl.fbaipublicfiles.com/fasttext/vectors-crawl/cc.en.300.vec.gz


and place then in ./data/vec/vectors-{bn.en}.txt
