# charity-funding-predictor

## Overview
This analysis was to create a neural net model for predicting an organization's likelihood of an applicant to succeed if funded. A csv file was provided as the dataset.

## Results
### Data Preprocessing
* The target of this dataset was the variable `IS_SUCCESSFUL`.
* The features of this dataset were the variables...
    * `APPLICATION_TYPE`
    * `AFFILIATION`
    * `CLASSIFICATION`
    * `USE_CASE`
    * `ORGANIZATION`
    * `INCOME_AMT`
    * `SPECIAL_CONSIDERATIONS`
    * `ASK_AMT`
* The variable `STATUS` was removed from the dataset for the optimized model. Reasoning is explained later in this document.

### Compiling, Training, and Evaluating the Model
* The initial model used the following parameters...
    * Two hidden layers with 80 and 30 neurons respectively. Both used the `relu` activation function.
    * One output layer with 1 neuron that used the `sigmoid` activation function.
* The optimized model used the following parameters...
    * Two hidden layers with 6 and 2 neurons respectively. Both used the `sigmoid` activation function.
    * One output layer with 1 neuron that used the `sigmoid` activation function.

### Results
My attempt at optimizing the model included two phases. The first phase was to determine the most impactful configuration of excluded columns and binning cutoff values. To acquire these values I built a nested loop to explore the different combinations and evaluate each one using the same neural network model. Presumably the best performing (highest accuracy) result belonged to the most impactful combination. The second phase was use the most impactful combination as the input for a `KerasTuner` optimization. The optimization returned the hyperparameters stated above. Unfortunately the optimized model only reached an accuracy of `73.5%`, which is below the target accuracy of `75%`.

### Summary
It is my suspicion that the provided dataset might have been underfit for the attempted model. I suspect this due to the difficulty in increasing model accuracy when removing variables. I hadn't attempted it, but it might be worth trying at some point to increase one or two more layers to the impactful configuration search. Perhaps more than one feature had to be removed for improved performance.

A Random Forests classifier may outperform this neural net due to its high performance as a classifier. Seeing as we might have been fighting overfitting, a Random Forests classifier would have ignored the overfitting. Additionally, the ability of the classifier to point out more important features would have provided valuable insight for the previous steps. The insight from using this classifer in parallel would have been useful.