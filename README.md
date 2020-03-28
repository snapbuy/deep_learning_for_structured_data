# deep_learning_for_structured_data
revised repo for Manning book **Deep Learning with Structured Data** https://www.manning.com/books/deep-learning-with-structured-data

## Note
This repo is a rework of the original repo for the book at https://github.com/ryanmark1867/manning (which is being kept in place for the convenience of MEAP users who have already started to use it. Improvements in this new repo include:
- rationalized file names
- simplified directory structure
- notebooks tested on Python 3.6 and Python 3.7 in free and for-fee environments
- config files used to remove hard-coded parameters
- code largely refactored to make it easier to follow and simpler to run

## Directory structure
- **data** - processed datasets and pickle files for intermediate datasets
- **deploy** - code for deploying the trained model using Rasa and Facebook Messenger, as described in chapter 8 of the book
- **deploy_web** - code for deploying the trained model via a simple web page served by Flask. Description coming in chapter 8.
- **models** - saved trained models
- **notebooks** - Jupyter notebooks **streetcar_data_preparation.ipynb** (data preparation) and **streetcar_model_training.ipynb** (model training) along with associated class and config files
- **pipelines** - pickled pipeline files generated by **streetcar_model_training.ipynb**. Together with the trained models these pipeline files are used in the deployment.
- **sql** - SQL used to generate a table that can be used for the simple SQL examples in chapter 5

## To exercise the code
**prepare data** - steps to clean up input data to prepare it to train a deep learning model. Output is a pickled dataframe containing the cleaned up dataset.
1. update **notebooks/streetcar_data_preparation_config.yml**  to specify name of input data (pickled_input_dataframe if load_from_scratch = False; if load_from_scratch = True then copy xls files from https://open.toronto.ca/dataset/ttc-streetcar-delay-data/ to **data** directory) and output dataframe
2. run **notebooks/streetcar_data_preparation.ipynb**

**train model** - steps to train a deep learning model on the cleaned up dataset from the previous step. Output is a trained model (h5 file) and two pickle files for the pipeline 
1. update **notebooks/streetcar_model_training_config.yml** to specify input dataframe (pickled_dataframe). Set this to the filename of the dataframe output in the **prepare data** step
2. run **streetcar_model_training.ipynb** in an env. with TensorFlow 2.0 installed

**deploy model** - steps to set up a simple web page for exercising the trained model. Uses the trained model and pipeline files from the previous step.
1. update **deploy_web/deploy_web_config.yml**: set  pipeline1_filename, pipeline2_filename and model_filename to the names of the pipeline files and trained model file generated in the training step. Alternately, you can run the training notebook using the config file as-is to use prepared pipeline and model files already included in the repo.
2. start the Flask server **deploy_web/flask_server.py** by running: python flask_server.py
3. open localhost:5000 in a browser, select the details for your trip, and click on **Get prediction**
   
## Background

- **https://open.toronto.ca/dataset/ttc-streetcar-delay-data/** original dataset
- **https://www.kaggle.com/knowledgegrappler/a-simple-nn-solution-with-keras-0-48611-pl** Kaggle submission that was used as input to creation of the Keras model used in this example
d in this example