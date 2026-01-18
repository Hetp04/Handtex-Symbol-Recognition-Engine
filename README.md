# Handtex - Converting Handwritten Mathematical Expressions into LATEX

Handtex is a React App that lets users upload their handwritten mathematical images which are fetched via API and run through a convolutional neural network to accurately predict handwritten expressions and converted to strings of LATEX.

## Example

<div align="center">
  <img src="readme_images/pie.png">
</div>

## How It Works

It first uses object segmentation to extract the symbols from a given expression. With these extractions (called region's of interest or ROI for short), we load and resize them to prepare them for the CNN. The model is given these resized ROI's and predicts each symbol. The predictions are translated to their equivalent LATEX form and then outputed.

<p float='left'>
  <img src="readme_images/object_segmentation.png" width="300" height="200" />

  <img src="readme_images/object_resizing1.png" width="200" height="200" />

  <img src="readme_images/object_resizing2.png" width="200" height="200" />
</p>

![](readme_images/prediction.png)


## Dataset
I used the [CROHME dataset from Kaggle uploaded by Xai Nano](https://www.kaggle.com/datasets/xainano/handwrittenmathsymbols). With over 380,000 images, I utilized an 80/20 split for training/testing respectively. This dataset was trained on a convolutional neural network (CNN) which resulted in a 97% accuracy on testing data.

## Model Results

Here are graphs and results from testing the model on images its never seen before.

```python
testing_loss, testing_accuracy = model.evaluate(testing_images, testing_labels, verbose=2)
print(testing_accuracy)
```
```
1/1 - 0s - loss: 0.0925 - accuracy: 0.9688
0.96875
```
![](readme_images/accuracy_plot.png)

![](readme_images/loss_function_plot.png)


## Installation

You do not need the react app to run this project. Simply add images you wish to convert into a directory of your choosing and run the following command in the `server/predict.py` file.

```python
predict('dir/to/image') 
``` 

To run the CNN locally, just download the `models` folder and load the model with the following command:

```python
import tensorflow
tensorflow.keras.models.load_model('models')
``` 

To run the React App, download the **Handtex-React** folder and run:

```bash
cd client
npm install
npm start
``` 
