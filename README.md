# deep-learning-challenge

## Overview


Greetings,

Welcome to the ‘deep-learning-challenge’ repository! For this project, we were supplied a comprehensive features dataset (34,000+ entries) surrounding a nonprofit foundation’s applicant venture funding program with an included binary classifier label that indicates whether or not the instance was successful. Using this dataset, several neural networks were trained and tested to generate a binary classifier that can predict whether applicants will be successful.

## Repository Structure

"Initial_Model" Directory - Contains all files associated with the initial algorithm
- "Deep_Learning_Challenge.ipynb" - Jupyter Notebook with executed code for initial neural network model
- "Initial_Model_Weights" Folder - Contains saved initial model weights as .keras files
- "AlphabetSoupCharity.keras" - Initial neural network model
- "Initial_Accuracy.png"
- "Initial_Loss.png"


"Optimized_Models" Directory - Contains all files associated with the two subsequent optimized algorithms
- "AlphabetSoupCharity_Optimization.ipynb" - Jupyter Notebook with executed code for (2) subsequent optimized models
- "AlphabetSoupCharity_Manual_Optimization.keras" - Mannually optimized neural nework model
- "AlphabetSoupCharity_KerasTuner_Optimization.keras" - Keras Tuner optimized neural network model
- "Optimized_Accuracy.png"
- "Optimized_Loss.png"

## Results

**Data Preprocessing:**

Our model's target variable is most likely the binary identifier column "IS_SUCCESSFUL", which provides a (0) for an unsuccessful applicant venture and a (1) for a successful applicant venture. Conversely, all other columns containing relevant attribute information will represent the feature variables for our model (This does not include arbitrary identifiers such as "EIN" and "NAME", which will be removed).

Columns with 10 or more categorical values were bucketed/binned and subsequently the DataFrame was encoded via pd.get_dummies. The data was then split for training/test sets and appropriately scaled for model generation.

**Compiling, Training and Evaluating the Model(s):**

For the initial model, I chose to generate a neural network with 3 total layers. The first input layer with 80 neurons, an activation function of ReLU and 43 input dimensions to match our features array. The second layer with 30 neurons and an activation function of ReLU and finally the third output layer with a single unit and a Sigmoid activation function. This structure was executed given the likely complex nature of the data (multiple layers) and the high number of input features (higher starting neural density to align with 2-3x # of inputs). ReLU activation functions were used as a starting point for hidden layers and a Sigmoid activation function was used for the output layer as our target/model is a binary classifier.

_The initial predictive model achieved an accuracy of 0.7293 with a loss of 0.5603. In an effort to enhance the algorithm and achieve the target performance of 75%, the following specific optimization techniques were used manually:_

### Manual Optimization:

- **DATA:**

  - **OVERFITTING CONSIDERATIONS** (Unbalanced data, Unbalanced label/output representation between train/test, Model convergence):

    - Shift traditional 75/25 train/test split to 80/20

  - **UNDERFITTING CONSIDERATIONS** (High bias/little relation):

    - Outlier detection and removal within the 'ASK_AMT' column, which includes the highest variance amongst its values for entire dataset

- **MODEL:**

  - **Neuron/Node Count**

    - Increasing Neuron/Node units across the first layer to = roughly 2-3x the number of input dimensions (43) - changing from 80 to 120. As the initial model's performance indicates our data is likely complex, we will include only a slight adjustment to the number of neurons for the second layer (from 30 to 50).

  - **Hidden Layer Count**

    - Increasing the overall hidden layer count from (2) to (4) for increased perceptron interaction. With complex, likley non-linear data, more hidden layers typically perform better than less layers with more neurons. Note: the number of neurons for these third and fourth layers are initially set to match the second layer's with (50) each.

  - **Training Epoch Count**

    - As our initial model indicates, we're achieving fluctuating returns for primarily accuracy (loss as well) above 80 Epochs. As such, we will increase  this number to 150 and note the response.

  - **Activation Function**

    - Replacing our neural layer's activation functions with Tahn, instead of ReLU could provide a slight predictive boost. This could be attributed to the scaled nature of our input data containing values from -1 to 1, as the ReLU activation function forgoes negative outputs.


_The subsequent manually optimized model achieved the following metrics after the above techniques: Loss - 0.5414, Accuracy - 0.7513._

### Keras-Tuner Optimizaztion:

_The subsequent Keras-Tuner optimized model achieved the following metrics: Loss - 0.5408, Accuracy - 0.7484._


## Summary 

Please see the above accuracy and loss metrics for all models. Given this data, I would very loosely rely on this model’s ability to predict whether or not a potential applicant’s venture will ultimately be successful given all required inputs. While an accuracy of roughly 73-75% may indeed provide some usable insight during the approval process, this weak predictive capability coupled with a high loss metric of roughly 0.55, doesn’t inspire overall algorithm confidence.

As numerous optimization strategies including Keras Tuner failed to achieve any significant delta in either accuracy or loss metrics, I would suggest the true refinement regarding a predictive model lies less so in the model itself and much more so in the integrity of the dataset. Given the nature of the data especially in terms of the output/desired label referring to a broad classification of ‘successful’ or ‘not successful’ within the business realm, there naturally exists a confounding amount of variables that aren’t captured within the input metadata. Thus, I would emphasize increased data collection and more specifically the collection of relevant attributes.

Regarding an alternative modeling approach to this task, a more straightforward random forest algorithm could be executed in order to determine feature importance metrics. This data could uncover useful information on how to adjust data collection (or restructure data), which could in turn lead to/be used to build a more predictive model in the future.


## Initial Model (1st Two Images) vs. Manually Optimized Model (2nd Two Images) (Accuracy & Loss Images)

![Initial_Accuracy](https://github.com/user-attachments/assets/7b216a8a-1616-439a-b6da-812f79d5f253)
![Initial_Loss](https://github.com/user-attachments/assets/d2aacf2b-0910-48ad-a09b-6aaa7a861f94)

![Optimized_Accuracy](https://github.com/user-attachments/assets/013279ed-983c-454e-9bc4-7293f31a4c5b)
![Opitmized_Loss](https://github.com/user-attachments/assets/45251e79-d7d8-4a44-8f24-88250f3e6ee2)




