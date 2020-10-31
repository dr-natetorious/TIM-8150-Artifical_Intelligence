# Cat vs Dog Experiment

This experiment classifies images as either cat or dog.  It follows the [Image Classification from Scratch](https://keras.io/examples/vision/image_classification_from_scratch/) example from Keras.

## Setup notes

The `image_dataset_from_directory` function is only available in version 2.4.  According to [Keras Issue 12](https://github.com/keras-team/keras-io/issues/12), the resolution is to install the nightly build.  It sounds like this the additional pip step will go away around end of 2020.

```bash
pip install tf-nightly
curl -O https://download.microsoft.com/download/3/E/1/3E1C3F21-ECDB-4869-8368-6DEBA77B919F/kagglecatsanddogs_3367a.zip
unzip -q kagglecatsanddogs_3367a.zip
```
