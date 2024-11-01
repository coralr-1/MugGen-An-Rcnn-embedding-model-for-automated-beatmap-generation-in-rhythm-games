# MugGen

###### Utilize AI to create maps(charts) for rhythm games.



## Introduction

MugGen is a model based on convolutional neural networks that primarily generates 4k drop-style charts for the rhythm game 'malody'. Given an audio track, the model is able to produce a corresponding 4k chart.

The model boasts fast training and generation speeds, allowing it to generate charts of any length based on the music.On a 4060 Laptop GPU, it takes approximately 5 seconds to generate a 5-minute chart, requiring less than 1GB of graphics memory for chart generation alone.

In the future, MugGen may provide options for difficulty levels, key types, and optimizations in chart details.



## Install

Execute the following code on the command line to install the required libraries：

```
pip install -r requirements.txt
```



### Running

1. Unzip the chart file (.mcz, containing the chart .mc and audio files) and place it under folder  `1`. (To batch unzip, you can place the .mcz chart files directly into the `beatmap` folder of the Malody directory and then launch Malody, which will automatically unzip the .mcz files. After that, you can move the unzipped files to the folder named '1' in your code directory.)
2. Run all code blocks in `get_labels & data_operation.ipynb`. The code will convert the chart files into one-hot encoded arrays and store them in `.npy` files in the same directory as the chart (.mc files).
3. First, run `model_T_train.ipynb`. The third code block will convert the audio files into mel spectrograms, read the corresponding chart one-hot encoded data, and store them in a list format in the `train data` folder as `.pkl` files. The subsequent code blocks will train and save the model under `model\N`.
4. Then, run `model_T_train.ipynb` again, but this time the code blocks will train and save the model under `model\T`.
5. To generate charts, use `main.ipynb`. It has parameters that specify the model to use, the path and name of the audio to generate (I have preset a `music` folder where you can place the audio files you want to predict and then change the `music_name` parameter in the code). The generated charts and audio will be merged in the same folder and stored in `export`. You can directly move the generated folder to the `beatmap` folder in the Malody game directory.

## Others

Since the amount of your data is relatively small, the code for processing the charts only handles 100 charts, with the first 80 as the training set, 81-90 as the validation set, and 91-100 as the test set. If you need to modify the amount of data being processed, please adjust the third code block in `model_T_train.ipynb` as well as the code related to reading data during the training of the two models.