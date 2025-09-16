# Predicting Volumetric Efficiency values with a small scale neural network in PyTorch

This is a project I have worked on over the past year that has gone through several iterations and changes.
The goal of the project is to create a model that is able to accurately infer volumetric efficiency values by using data gained through ECU logs.
This model cannot 100% accurately demonstrate how a neural network deployed by car manufacturers would react on potential changes in readout data, as the models, frameworks and techniques they are using are generally opaque.
It still serves as an interesting demonstration and could help draw conclusions on how neural networks in ECU's work.

Constraints:
* The neural network has to be as small as possible to potentially run on embedded hardware like a piggyback ECU (or a raspberry) in real time.
* As I (unfortunately) do not own a programmable ECU I was working with limited training data, I had to make the most out of it by using the right features.

TODO:
* Check the pressure ratio values, they do not correlate with anything else after reading the csv with pandas.
* Retrain and evaluate the model using pressure ratio instead of Aircharge in milligrams
* Check inference speed on low powered hardware

Model performance:
* Huber Loss during training: 0.1598
* Huber Loss during evaluation: 0.1596

Model seems to perform on par with what is to be expected on unseen data.

File description:
* VE_model_training.ipynb - Model training notebook
  * train_split1.csv - Training data part 1
  * train_split2.csv - Training data part 2 (split due to github file size constraints)
* VE_model_training.ipynb - Model inference notebook
  * testdf_filtered.csv - prepared unseen testdata for further evaluation
  * vemodel_scripted.pt - scripted PyTorch model data
  * x_scaler.pkl - scaler data used during training
  * features.json - features used during training in the right order

# How to use:
Simply open up the desired Jupyter notebook and run it. Take the requirements.txt into consideration. You need the required packages.
The inference notebook will load a model that I pretrained whether you trained it yourself by running the training notebook beforehand or not.

You can of course try and replace the testdf_filtered.csv with your own data, keep the metrics and column order and names in mind.
