# Neural Network Charity Analysis

## Overview of the analysis
The purpose of this work is to create a binary classifier logic capable of predicting if a foundation/organization will be successful if it is funded by the company Alphabet Soup.
The neural network will be based on a dataset containing more than 34,000 organizations that have received funding from Alphabet. The data has details about: application type, income amount, classification, and other parameters. For data analysis purposes, some of the columns will be removed to improve the performance of the neural network. 

## Results

### Data Preprocesing.
- The variable considered as target for the model was the column "IS_SUCCESSFUL"  because it contains the final result, if the founding was successful or not. 
- All the other columns are considered as features.
- During the first analysis, we identified two columns that will not bring any benefits to the logic: "EIN" and "NAME". These columns are "labels", they don't contain any substantial or statistical information.


### Compiling, Training and evaluating the model.
- The first model started with two hidden layers. The first with 80 nodes (activation function ReLu) and the second with 30 nodes (ReLu function as well). The number of hidden layers can be defined by multiple reasons, but as a rule of thumb we can considered two conditions: 2/3 the size of the input layer plus size of the output layer, or less than twice the size of the input layer. For this case, the input (columns) is 44 which sets the limit for the hidden layers in 88. 
- The result for this first model was: 62 %.
- In order to improve the performance, we started by removing 4 additional columns : 
  * APPLICATION_TYPE : Alphabet application type. It seems like it is related to internal registration process.  
  * SPECIAL_CONSIDERATIONS : only two possible results.
  * STATUS :  Only two possible results
  
  Then we executed 5 different options with different layers and differen activation functions: 


|          |   # of hidden layers   |              function                          |    epoch   |   result   |      
|----------|------------------------|------------------------------------------------|------------|------------|
| Option 1 |            3           |      RELU-64, RELU-32, RELU-16                 |     50     |    53 %    |   
| Option 2 |            4           | RELU-80, RELU-40, leaky_RELU-20, leaky_RELU-10 |     50     |    55 %    |             
| Option 3 |            2           |      leaky_RELU-40, leaky_RELU-20              |     50     |    54 %    |       
| Option 4 |      RANDOM FOREST     |                 -                              |     -      |    63%     |
| Option 5 |            3           |      RELU-64 , tanh-32, leaky_Relu-16          |     50     |    53 %    |  

Leaky_Relu was tested becase this function overcome one of the major shortcomings of ReLu. When the value is negative in ReLu, no learning happens. To avoid this issue, researches created the Leaky_Relu. ( ref: https://www.quora.com/What-are-the-advantages-of-using-Leaky-Rectified-Linear-Units-Leaky-ReLU-over-normal-ReLU-in-deep-learning)

## Summary 
- Despite of the multiple tests, we could not achieve a 75% of perfomance.  The highest values that we obtained was using the Random Forest (this module was selected as reference) and when I combined 4 hidden layers. 
- We can continue analyzing other function combination and increasing the number of hidden layers to improve the perfomance, however we may need increase the size of hte dataset to train our modules. 
- Based on the results it seems like Random Forest could be a better solution for this particula case.
