# **CRUST** (Chungus Related Uberduck's Speech toy)
# Welcome to Crust.

Crust is a 168 speaker model based on uberduck's pipeline. We've noticed that having multiple speakers instead of having one speaker, improves the performance of the model and makes it be able to synthesize comparable results with only 1 minute of data. The results are surprisingly good and because of the lower dataset, batch size can be lowered and the model is generally faster than other models.

### What is a multispeaker model?

A multispeaker model is a model that has been trained on multiple speakers, the model first generates an "average" voice of all of the speakers and then tunes the different speakers on that average voice. If you have a lot of speakers, individual results won't be that great, as the model only has ~250+ mb to work with, but this is great for finetuning different voices on it because the model has learned an "average" voice. This average voice has the knowledge of all voices included in the dataset.

### How does this make training possible with 1 minute of training data?

The model has been trained on 168 datasets, ~20 hours of data, or ~19.8 thousand audio files. This is smaller than LJ speech but it has way more variety in voices, which LJ speech doesn't have. this variety allows the model to learn speech in different genders, accents, pitches, and other important factors, meaning that it knows a lot more in terms of voices. Finetuning this on 1 minute of data is possible because it already has a decently close match of your voice somewhere in its latent space.

### What are the downsides?

**-Training time.**

Training time sadly does still take a while, but considering you might only be training using 1 minute of data, it would take shorter than training it on the Lj-speech model, but would not come close to corentj's realtime voice cloning, it would be more accurate.

**-Clean datasets.**

We still doubt if the model would be able to be trained on datasets that have loud noise in them or have background music in them, realistically, it would not be able to be trained on these kinds of datasets, so before you train, please use a clean dataset.

**-Inference.**

Even though this model can be trained on 1 minute of data, we still recommend training it on more, we can't promise good results if the model doesn't have sufficient data, this would ideally be measured in syllables or phonemes, but minutes is a lot easier.

**-Audio quality.**

Sadly, the model has only been trained on 22050 hz and mono audio files, while this still sounds good when there's a Hi-Fi Gan vocoder, It's still going to not have stereo sound (which would not be that useful) or 44100 hz audio quality on its own. Sadly the Hi-Fi Gan vocoder does also bring in artifacts into the wav files which makes synthesis not as realistic.
































# 🦆 Uberduck TTS ![](https://img.shields.io/github/forks/uberduck-ai/uberduck-ml-dev) ![](https://img.shields.io/github/stars/uberduck-ai/uberduck-ml-dev) ![](https://img.shields.io/github/issues/uberduck-ai/uberduck-ml-dev)



<h1>Table of Contents<span class="tocSkip"></span></h1>
<div class="toc"><ul class="toc-item"><li><span><a href="#🦆-Uberduck-TTS---" data-toc-modified-id="🦆-Uberduck-TTS----1"><span class="toc-item-num">1&nbsp;&nbsp;</span>🦆 Uberduck TTS <img src="https://img.shields.io/github/forks/uberduck-ai/uberduck-ml-dev" alt=""> <img src="https://img.shields.io/github/stars/uberduck-ai/uberduck-ml-dev" alt=""> <img src="https://img.shields.io/github/issues/uberduck-ai/uberduck-ml-dev" alt=""></a></span><ul class="toc-item"><li><span><a href="#Installation" data-toc-modified-id="Installation-1.1"><span class="toc-item-num">1.1&nbsp;&nbsp;</span>Installation</a></span></li><li><span><a href="#Development" data-toc-modified-id="Development-1.2"><span class="toc-item-num">1.2&nbsp;&nbsp;</span>Development</a></span><ul class="toc-item"><li><span><a href="#🚩-Testing" data-toc-modified-id="🚩-Testing-1.2.1"><span class="toc-item-num">1.2.1&nbsp;&nbsp;</span>🚩 Testing</a></span></li></ul></li><li><span><a href="#📦️-nbdev" data-toc-modified-id="📦️-nbdev-1.3"><span class="toc-item-num">1.3&nbsp;&nbsp;</span>📦️ nbdev</a></span><ul class="toc-item"><li><span><a href="#🔧-Troubleshooting-Tips" data-toc-modified-id="🔧-Troubleshooting-Tips-1.3.1"><span class="toc-item-num">1.3.1&nbsp;&nbsp;</span>🔧 Troubleshooting Tips</a></span></li></ul></li><li><span><a href="#Overview" data-toc-modified-id="Overview-1.4"><span class="toc-item-num">1.4&nbsp;&nbsp;</span>Overview</a></span></li></ul></li></ul></div>

[**Uberduck**](https://uberduck.ai/) is a tool for fun and creativity with audio machine learning, currently focused on voice cloning and neural text-to-speech. This repository includes development tools to get started with creating your own speech synthesis model. For more information on the state of this repo, please see the [**Wiki**](https://github.com/uberduck-ai/uberduck-ml-dev/wiki).

## Installation

```
conda create -n 'uberduck-ml-dev' python=3.8
source activate uberduck-ml-dev
pip install git+https://github.com/uberduck-ai/uberduck-ml-dev.git
```

## Development

To start contributing, install the required development dependencies in a virtual environment:

```bash
pip install nbdev nbqa pre-commit
```

Then install required Git hooks:

```bash
nbdev_install_git_hooks
pre-commit install
```

All development takes place in Jupyter notebooks in `$REPO_ROOT/nbs`, which are compiled to library code in `$REPO_ROOT/uberduck_ml_dev`. To make changes, edit edit the one of the IPython notebooks in `$REPO_ROOT/nbs/` after starting a jupyter server with `jupyter notebook`. Once you're satisfied with the changes, build them:

```bash
./build_lib
```

Then install the library
```bash
python setup.py develop
```

### 🚩 Testing

Any IPython notebook cell which is not exported is a test. Run all tests:

```bash
nbdev_test_nbs
```

Test a single notebook:

```bash
 nbdev_test_nbs --fname nbs/text.util.ipynb
 ```
 (can optionally add `--verbose` for more output)
 
 Annotate a notebook cell with the `#skip` flag if it is code which is neither a test nor library code.

## 📦️ nbdev

This project uses [nbdev](https://nbdev.fast.ai/).

_If you are using an older version of this template, and want to upgrade to the theme-based version, see [this helper script](https://gist.github.com/hamelsmu/977e82a23dcd8dcff9058079cb4a8f18) (more explanation of what this means is contained in the link to the script)_.

### 🔧 Troubleshooting Tips

-  Make sure you are using the latest version of nbdev with `pip install -U nbdev`
-  If you are using an older version of this template, see the instructions above on how to upgrade your template. 
-  It is important for you to spell the name of your user and repo correctly in `settings.ini` or the website will not have the correct address from which to source assets like CSS for your site.  When in doubt, you can open your browser's developer console and see if there are any errors related to fetching assets for your website due to an incorrect URL generated by misspelled values from `settings.ini`.
-  If you change the name of your repo, you have to make the appropriate changes in `settings.ini`
-  After you make changes to `settings.ini`, run `nbdev_build_lib && nbdev_clean_nbs && nbdev_build_docs` to make sure all changes are propagated appropriately.


## Overview

An overview of the subpackages in this library:

`models`: TTS model implementations. All models descend from `models.base.TTSModel`.

`trainer`: A trainer has logic for training a model.

`exec`: Contains entrypoint scripts for running training jobs. Executed via a command like
`python -m uberduck_ml_dev.exec.train_tacotron2 --your-args here`
