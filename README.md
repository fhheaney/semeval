semeval
=======

Semantic Textual Similarity (STS) system created by the MathLingBudapest team to participate in Tasks 1 and 2 of Semeval2015 and modified as part of a WPI 2017 Major Qualifying Project in Computer Science by Fiona Heaney (fhheaney) and Matt Zielonko (zoinks27) 


# Dependencies
First you need to install the SciPy stack on your machine by following instructions specific to your system on [this page](http://www.scipy.org/install.html)

Then run
```
sudo python setup.py install
```

Our pipeline relies on the TreeTagger tool for part-of-speech tagging, which can be downloaded from [this page](http://www.cis.uni-muenchen.de/~schmid/tools/TreeTagger/). All you need to do is download and place the tagger and Spanish parameter in the directory semeval/treetagger (or change the value of `treetagger_dir` in the configuration file to point to a different location).

In order to run the precompiled binaries on a 64-bit machine, you should download the 32-bit C library:
```
sudo dpkg --add-architecture i386 
sudo apt-get update
sudo apt-get install libc6:i386 
```

The machine similarity component also requires the 4lang module. To download and install it, follow [these instructions](https://github.com/kornai/4lang/blob/master/README.md). Then configure it by editing the configuration file `configs/sts\_machine.cfg` based on the instructions in the [4lang README](https://github.com/kornai/4lang/blob/master/README.md#the-config-file)

Some of our configurations also make use of word embeddings, to get the pre-trained models, just download [this archive](http://people.mokk.bme.hu/~recski/4lang/embeddings.tgz) and extract it in your `semeval` directory.

In order to download the required ntlk corpuses, use:
```
python -m nltk.downloader stopwords wordnet
```

# Usage

The STS system can be invoked from the repo's base directory using:

```
    cat spanish_sts_test.txt | python semeval/paraphrases.py -c configs/sts.cfg > out
```

This test file follows the format of the Semeval 2014 Task 10.

To use the machine similarity component, run

```
cat spanish_sts_test.txt | python semeval/paraphrases.py -c configs/sts_machine.cfg > out
```

## Regression used for Task 2 STS data

sample uses of regression.py:

     python scripts/regression.py regression_train all.model semeval_data/sts_trial/201213_all data/1213_all/ngram data/1213_all/lsa data/1213_all/machine

     for f in data/2014-test/nosim_4gr_d/STS.input.*; do topic=`basename $f | cut -d'.' -f3`; echo $topic; python scripts/regression.py regression_predict all.model data/2014-test/nosim_4gr_d/STS.input.$topic.txt.out data/2014-test/lsa_sim_bp/STS.input.$topic.txt.out data/2014-test/machine_sim_nodes2/STS.input.$topic.txt.out > data/2014-test/regr/STS.input.$topic.txt.out; done


##Reverting to the Semeval-2015 submission version
This code and its dependencies are under constant development. To run the version of the code that was used to create the MathLingBudapest team's submissions (although many bugs have been fixed since), use the following revisions:_

Task 1: https://github.com/juditacs/semeval/tree/submitted

Task 2: https://github.com/juditacs/semeval/tree/15863ba5bc7f857291322c707a899c7c802a7c88

If you'd also like to reproduce the machine similarity component as it was at the time of the submission, you'll need the following revision of the pymachine repository:

https://github.com/kornai/pymachine/tree/3d936067e775fc8aa56c06388eb328ef2c6efe75

## Contact
This repository is maintained by Judit Ács and Gábor Recski. Questions, suggestions, bug reports, etc. are very welcome and can be sent by email to recski at mokk bme hu.
Any questions regarding changes made in the forked version of this repo may be firected towards Fiona Heaney (fhheaney at wpi dot edu) and Matt Zielonko (mlzielonko at wpi dot edu)

### Publications
If you use the `semeval` module, please cite:

```
@InProceedings{Recski:2015a,
  author    = {Recski, G\'{a}bor  and  \'{A}cs, Judit},
  title     = {MathLingBudapest: Concept Networks for Semantic Similarity},
  booktitle = {Proceedings of the 9th International Workshop on Semantic Evaluation (SemEval 2015)},
  month     = {June},
  year      = {2015},
  address   = {Denver, Colorado},
  publisher = {Association for Computational Linguistics},
  pages     = {543--547},
  url       = {http://www.aclweb.org/anthology/S15-2086}
}
```
