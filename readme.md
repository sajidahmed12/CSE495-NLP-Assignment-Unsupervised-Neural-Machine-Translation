# Unsupervised Neural Machine Translation 
## Bangla To English, English To Bangla

* state-of-the-art multilingual word embeddings ([fastText](https://github.com/facebookresearch/fastText/blob/master/pretrained-vectors.md) embeddings aligned in a common space)
* large-scale high-quality bilingual dictionaries for training and evaluation

We include two methods, one *supervised* that uses a bilingual dictionary or identical character strings, and one *unsupervised* that does not use any parallel data (see [Word Translation without Parallel Data](https://arxiv.org/pdf/1710.04087.pdf) for more details).

## Dependencies
* Python >=3.5.0
* [NumPy](http://www.numpy.org/)
* Jupyter-Notebook
* gensim
* tqdm
* [SciPy](https://www.scipy.org/)
* [PyTorch](http://pytorch.org/)
* [Faiss](https://github.com/facebookresearch/faiss) (recommended) for fast nearest neighbor search (CPU or GPU).
* [MUSE](https://github.com/facebookresearch/MUSE)


## Get evaluation datasets
To download monolingual and cross-lingual word embeddings evaluation datasets:
* Our 110 [bilingual dictionaries](https://github.com/facebookresearch/MUSE#ground-truth-bilingual-dictionaries)
* 28 monolingual word similarity tasks for 6 languages, and the English word analogy task
* Cross-lingual word similarity tasks from [SemEval2017](http://alt.qcri.org/semeval2017/task2/)
* Sentence translation retrieval with [Europarl](http://www.statmt.org/europarl/) corpora

Simply run:

```bash
cd data/
wget https://dl.fbaipublicfiles.com/arrival/vectors.tar.gz
wget https://dl.fbaipublicfiles.com/arrival/wordsim.tar.gz
wget https://dl.fbaipublicfiles.com/arrival/dictionaries.tar.gz
```

Alternatively, you can also download the data with:

```bash
cd data/
./get_evaluation.sh
```

*Note: Requires bash 4. The download of Europarl is disabled by default (slow), you can enable it [here](https://github.com/facebookresearch/MUSE/blob/master/data/get_evaluation.sh#L99-L100).*

## Get monolingual word embeddings
For pre-trained monolingual word embeddings, we highly recommend [fastText Wikipedia embeddings](https://fasttext.cc/docs/en/pretrained-vectors.html), or using [fastText](https://github.com/facebookresearch/fastText) to train your own word embeddings from your corpus.

You can download the English (en) and Bangla (bn) embeddings this way:
```bash
# English fastText Wikipedia embeddings
curl -Lo data/wiki.en.vec https://dl.fbaipublicfiles.com/fasttext/vectors-wiki/wiki.en.vec
```
## Align monolingual word embeddings
(https://en.wikipedia.org/wiki/Orthogonal_Procrustes_problem) alignment.
* **Unsupervised**: without any parallel data or anchor point, learn a mapping from the source to the target space using adversarial training and (iterative) Procrustes refinement.

### The unsupervised way: adversarial training and refinement (CPU|GPU)
To learn a mapping using adversarial training and iterative Procrustes refinement, run:
```bash
python unsupervised.py --src_lang en --tgt_lang es --src_emb data/wiki.en.vec --tgt_emb data/wiki.es.vec --n_refinement 5
```
By default, the validation metric is the mean cosine of word pairs from a synthetic dictionary built with CSLS (Cross-domain similarity local scaling). For some language pairs (e.g. En-Zh),
we recommend to center the embeddings using `--normalize_embeddings center`.

### Evaluate monolingual or cross-lingual embeddings (CPU|GPU)
We also include a simple script to evaluate the quality of monolingual or cross-lingual word embeddings on several tasks:

**Monolingual**
```bash
python evaluate.py --src_lang en --src_emb data/wiki.en.vec --max_vocab 200000
```

**Cross-lingual**
```bash
python evaluate.py --src_lang en --tgt_lang es --src_emb data/wiki.en-es.en.vec --tgt_emb data/wiki.en-es.es.vec --max_vocab 200000
```

## Word embedding format
By default, the aligned embeddings are exported to a text format at the end of experiments: `--export txt`. Exporting embeddings to a text file can take a while if you have a lot of embeddings. For a very fast export, you can set `--export pth` to export the embeddings in a PyTorch binary file, or simply disable the export (`--export ""`).

When loading embeddings, the model can load:
* PyTorch binary files previously generated by MUSE (.pth files)
* fastText binary files previously generated by fastText (.bin files)
* text files (text file with one word embedding per line)

The two first options are very fast and can load 1 million embeddings in a few seconds, while loading text files can take a while.

## Download
We provide multilingual embeddings and ground-truth bilingual dictionaries. These embeddings are fastText embeddings that have been aligned in a common space.

##### Multilingual word Embeddings
We release fastText Wikipedia **supervised** word embeddings for **30** languages, aligned in a **single vector space**.

Bengali: [full](https://dl.fbaipublicfiles.com/arrival/dictionaries/bn-en.txt) [train](https://dl.fbaipublicfiles.com/arrival/dictionaries/bn-en.0-5000.txt) [test](https://dl.fbaipublicfiles.com/arrival/dictionaries/bn-en.5000-6500.txt) 

##### 1. Download the Vectors from these Fast Text vectors.
* i.  Bangla [vectors-bn.txt](https://dl.fbaipublicfiles.com/fasttext/vectors-crawl/cc.bn.300.vec.gz) 
* ii. English [vectors-en.txt](https://dl.fbaipublicfiles.com/fasttext/vectors-crawl/cc.en.300.vec.gz) 

##### 2. Then place these vectors in ./data/vec/vectors-{bn.en}.txt location. 
* Download src.pickle from this [Gdrive link](https://drive.google.com/file/d/19bGSyykc5oYeUwy7BJS6PFm0BSbnRrUa/view) and place in the root directory. 
* Download tgt.pickle from this [Gdrivelink](https://drive.google.com/file/d/1GuFLa9lAvzXxfpWkGspmxefQ_m544H5S/view) and place in the root directory. 
* Download all.pickle from this [Gdrivelink](https://drive.google.com/file/d/1SVsgUKXeGf3gbZmhqFwM3_mLgH5MB0ec/view) and place in the root directory. 

### Visualization of the multilingual word embedding space
[Similar word embeddings in same latent space for Bengali and English words](./docs/aaa.PNG)

## Testing the Model with Bilingual Translation

Download the trained_model.pt file from the following [link](https://drive.google.com/file/d/17-RFIitkcnphSQZ_CkxN_203laTO8lVH/view)
* English To Bangla Translation
* Run the following command to test and translate sample data. 

```bash
python3 translate.py -s data/eng_test.txt -sl e -t out_ben.txt
```
* Bangla To English Translation
* Run the following command to test and translate sample data. 

```bash
python3 translate.py -s data/ben_test.txt -sl b -t out_eng.txt
```

#### Contributors 
* Md Sajid Ahmed- 1610364042
* Zahin Akram- 1610618042
* Arifuzzaman Arman- 1610551042
* Md Rakib Imtiaz- 1610294642

#### 2. Contribution Per member:

* All 4 members of the group worked together in understanding the paper 
through by separate and then reading the paper together. All members together began
the training of word embedding through MUSE. It was Sajid and Zahin who looked at the 
code deeply and worked in editing the necessary portion of what was required. Sajid
later ran the model and generated the mapping that was later shown to professor Dr. Nabeel Mohammad.

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


### For any furthur query please feel free to contact me [Md Sajid Ahmed](mailto:[sajid.ahmed1@northsouth.edu) 
