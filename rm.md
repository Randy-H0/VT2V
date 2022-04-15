# **CRUST** (Chungus Related Uberduck's Speech toy)
# Welcome to Crust 🍕⭕

Crust is a 168 speaker model based on uberduck's pipeline. We've noticed that having multiple speakers instead of having one speaker, improves the performance of the model and makes it be able to synthesize comparable results with only 1 minute of data. The results are surprisingly good and because of the lower dataset, batch size can be lowered and the model is generally faster than other models.

### What is a multispeaker model?

A multispeaker model is a model that has been trained on multiple speakers, the model first generates an "average" voice of all of the speakers and then tunes the different speakers on that average voice. If you have a lot of speakers, individual results won't be that great, as the model only has ~250+ mb to work with, but this is great for finetuning different voices on it because the model has learned an "average" voice. This average voice has the knowledge of all voices included in the dataset.

Core: A multispeaker model is a model trained on multiple speakers.

### How does this make training possible with 1 minute of training data?

The model has been trained on 168 datasets, ~20 hours of data, or ~19.8 thousand audio files. This is smaller than LJ speech but it has way more variety in voices, which LJ speech doesn't have. this variety allows the model to learn speech in different genders, accents, pitches, and other important factors, meaning that it knows a lot more in terms of voices. Finetuning this on 1 minute of data is possible because it already has a decently close match of your voice somewhere in its latent space.

Core: The multispeaker has more knowledge of multiple people speaking, making it surprisingly good at training on low-minute datasets.

### What are the downsides?

**-Training time.**

Training time sadly does still take a while, but considering you might only be training using 1 minute of data, it would take shorter than training it on the Lj-speech model, but would not come close to corentj's realtime voice cloning, it would be more accurate.

**-Clean datasets.**

We still doubt if the model would be able to be trained on datasets that have loud noise in them or have background music in them, realistically, it would not be able to be trained on these kinds of datasets, so before you train, please use a clean dataset.

**-Inference.**

Even though this model can be trained on 1 minute of data, we still recommend training it on more, we can't promise good results if the model doesn't have sufficient data, this would ideally be measured in syllables or phonemes, but minutes is a lot easier.

**-Audio quality.**

Sadly, the model has only been trained on 22050 hz and mono audio files, while this still sounds good when there's a Hi-Fi Gan vocoder, It's still going to not have stereo sound (which would not be that useful) or 44100 hz audio quality on its own. Sadly the Hi-Fi Gan vocoder does also bring in artifacts into the wav files which makes synthesis not as realistic.

We used [**Uberduck's TTS Pipeline on github**](https://github.com/uberduck-ai/uberduck-ml-dev) To train our model.
