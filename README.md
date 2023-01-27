# Goal of the project :
### Guidelines for the projects :
This year, your assignment in the projects is to choose an article from the list provided below, understand it, and, most importantly, try to replicate the experiments.

Rules are as follows:

    Projects are conducted by team of 4 students. Team members are responsible for decompose the work so that all members contribute meaningfully to the project.

The following deliverables are expected:

    Before ( January 12th 2023 ), the choice of the paper and the names of the members of the team.
    ( February, 22nd 2023 ) Final report : 10 pages (strict. Reports longer than 10 pages will not be read!)

The interlediary report and the final reports must be turned down in the ICML (Int. Conf. on Machine Learning) format for papers. The deliverables will be evaluated taking into account:

    The clarity of the analysis of the chosen article. The paper should briefly present, in no more than two to four pages (out of the 10 allotted), the problem studied in the article, the main ideas and statements presented in the paper. The remaining pages will present the experiments carried out by the team, the possible difficulties, the results obtained and a comparison with the results presented by the authors of the article used as a basis for the project.

    The rigor and the extensive character of the analysis and/or the experiments carried out. A project that really answers the questions and possible doubts of the reviewers on the interest of the method and on the announced performances will obtain a higher score.

    Expression, clarity of explanation and quality of exposition. Reports can be written in French or English, as long as they are clear and well written.




<br/>------------------------------------------------------------------------------------------------






# Friendly Training - AAAI 2022
Title: **Being Friends Instead of Adversaries: Deep Networks Learn to Simplify Data to Train Other Networks**
Authors: Simone Marullo, Matteo Tiezzi, Marco Gori, Stefano Melacci

_Notice that reproducibility is not guaranteed by PyTorch across different releases, platforms, hardware. Moreover, determinism cannot be enforced due to use of PyTorch operations for which deterministic implementations do not exist (e.g. bilinear upsampling)._

Make sure to have Python dependencies (including PyTorch) by running:
```
pip install -r requirements.txt
```

## Datasets
CIFAR-10 is publicly available (automatic download in `data` directory).

MNIST Variations and geometric shapes **[2]** are available at http://www.iro.umontreal.ca/~lisa/icml2007data (downloader script in `download_larochelle.sh`).

Wines reviews are available on [Kaggle](https://www.kaggle.com/zynicide/wine-reviews). The original data are included in `data` directory. Text vectorization should be performed by running the Python script `data/wines_data_processing.py`.

IMDB reviews are available at [stanford.edu](http://ai.stanford.edu/~amaas/data/sentiment/). Downloader script is available (see `download_imdb.sh`). Text vectorization should be performed by running the Python script `data/imdb_data_processing.py`.


## Launching experiments
Neural Friendly Training experiments can be launched with the `train-neural.py` Python script.

On the other hand, experiments with the FT approach (see Supplementary material and **[1]** for details) can be run with `train-delta.py`.

Example commands are available in the `scripts` directory (run them from the root directory). See `commands_advanced-digit-and-shape-recognition.sh`, `commands_image-classification.sh`, `commands_sentiment-analysis.sh` to repreduce results reported in the tables of the paper.

## Differences with the paper text
Algorithm 1 of paper text (NFT) is implemented in `train-neural.py` (optimization phases are swapped but equivalent).
Names of command line parameters slightly differ with respect to paper text, hence we report the name mapping (more details in the code).

Parameter $\frac{\gamma_{max\_{simp}}}{\gamma_{max}}$ is called `ratio_simp`, $\gamma_{max}$ corresponds to `epochs`.
Concerning the U-Net simplifier, $\nu$ is called `n_deep`, $n_f$ is `n_filters_base`.
$\alpha$, $\beta$ are termed `lr_clf`, `lr_simp`. $\eta_{max}$ is called `beta_simp`.

We implemented FT algorithm (see **[1]**) in `train-delta.py`.
$\frac{\xi_{max\_{simp}}}{\gamma_{max} |B|}$ is named `ratio_simp`, while $c$ is `conf_thres`.
$\alpha$ is referred to as `lr`, $\beta$ is `step_simp`.

Architectures FC-A, FC-B, CNN-A, CNN-B, ResNet18 are named `ff`, `ff2`, `cnn`, `cnn2`, `resnet`.

## References
**[1]** Marullo, S.; Tiezzi, M.; Gori, M.; and Melacci, S. 2021.
Friendly Training: Neural Networks Can Adapt Data To Make Learning Easier. 
In IEEE International Joint Conference on Neural Networks (IJCNN) (arXiv preprint arXiv:2106.10974).

**[2]** Larochelle, H.; Erhan, D.; Courville, A.; Bergstra, J.; and Bengio, Y. 2007.
An empirical evaluation of deep architectures on problems with many factors of variation. 
In International Conference on Machine Learning, 473–480.
