Group bleeding
simple to understand, interpret, visualize
can handle both numerical and categorical
can handle missing data
no need of normalization
robust to outliers
can be trained on large data sets
requires little data preparation
can model non-linearity in dataset
Disadvantages
large trees hard to interpret
high variance - poor model performance
trees overfit easily

response variable is modeled as a function of all other variables
. means all other variables

Evaluation metrics for binary classification
accuracy
confusion matrix
log-loss
Area under curve


Regression trees - numeric output
validation set - used to measure models performance on unseen data
tune hyper parameters, choose best model among different options

### Random Samples And Permutations
- sample takes a sample of the specified size from the elements of x using either with or without replacement.

Arguments
x
either a vector of one or more elements from which to choose, or a positive integer. See ‘Details.’

n
a positive number, the number of items to choose from. See ‘Details.’

size
a non-negative integer giving the number of items to choose.

replace
should sampling be with replacement?

prob
a vector of probability weights for obtaining the elements of the vector being sampled.

# Set seed and create assignment
set.seed(1)
assignment <- sample(1:3, size = nrow(grade), prob = c(0.7,0.15,0.15), replace = TRUE)
assignment
# Create a train, validation and tests from the original data frame 
grade_train <- grade[assignment == 1, ]    # subset grade to training indices only
grade_valid <- grade[assignment == 2, ]  # subset grade to validation indices only
grade_test <- grade[assignment == 3, ]   # subset grade to test indices only	

### Classification Trees Performance Metrics
- Mean Absolute Error (MAE)
- Root Mean Suare Error (RMSE) More useful when large errors are undesirable

Use case dependent
R package Metrics

### Hyperparameters for decision trees
rpart.control 
- minsplit: min no of data points required to attempt a split
- cp: cost - complexity parameter
smaller cp -> more complex tree
plotcp(data)
xerror is minimized in cp table
prune function to tune or trim the model

```
# Plot the "CP Table"
plotcp(grade_model)

# Print the "CP Table"
print(grade_model$cptable)

# Retrieve optimal cp value based on cross-validated error
opt_index <- which.min(grade_model$cptable[, "xerror"])
cp_opt <- grade_model$cptable[opt_index, "CP"]

# Prune the model (to optimized cp value)
grade_model_opt <- prune(tree = grade_model, 
                         cp = cp_opt)
                          
# Plot the optimized model
rpart.plot(x = grade_model_opt, yesno = 2, type = 0, extra = 0)
```
### Model selection or hyperparameter selection
Grid Search
-Grid combination of hyperparamteres to find the best model


```
# Establish a list of possible values for minsplit and maxdepth
minsplit <- seq(1, 4, 1)
maxdepth <- seq(1, 6, 1)

# Create a data frame containing all combinations 
hyper_grid <- expand.grid(minsplit = minsplit, maxdepth = maxdepth)

# Check out the grid
head(hyper_grid)

# Print the number of grid combinations
nrow(hyper_grid)
```

Sequence Generation
Generate regular sequences. seq is a standard generic with a default method. seq.int is a primitive which can be much faster but has a few restrictions. seq_along and seq_len are very fast primitives for two common cases.
from, to
the starting and (maximal) end values of the sequence. Of length 1 unless just from is supplied as an unnamed argument.

by
number: increment of the sequence.

### Create A Data Frame From All Combinations Of Factor Variables
expand.grid() - Create a data frame from all combinations of the supplied vectors or factors. See the description of the return value for precise details of the way this is done.

```

# Number of potential models in the grid
num_models <- nrow(hyper_grid)

# Create an empty list to store models
grade_models <- list()

# Write a loop over the rows of hyper_grid to train the grid of models
for (i in 1:num_models) {

    # Get minsplit, maxdepth values at row i
    minsplit <- hyper_grid$minsplit[i]
    maxdepth <- hyper_grid$maxdepth[i]

    # Train a model and store in the list
    grade_models[[i]] <- rpart(formula = final_grade ~ ., 
                               data = grade_train, 
                               method = "anova",
                               minsplit = minsplit,
                               maxdepth = maxdepth)
}
```

```
A dataset that is not used in training is sometimes referred to as a "holdout" set. A holdout set is used to estimate model performance and although both validation and test sets are considered to be holdout data, there is a key difference:

Just like a test set, a validation set is used to evaluate the performance of a model. The difference is that a validation set is specifically used to compare the performance of a group of models with the goal of choosing a "best model" from the group. All the models in a group are evaluated on the same validation set and the model with the best performance is considered to be the winner.
Once you have the best model, a final estimate of performance is computed on the test set.
A test set should only ever be used to estimate model performance and should not be used in model selection. Typically if you use a test set more than once, you are probably doing something wrong.
```

```
# Number of potential models in the grid
num_models <- length(grade_models)

# Create an empty vector to store RMSE values
rmse_values <- c()

# Write a loop over the models to compute validation RMSE
for (i in 1:num_models) {

    # Retrieve the i^th model from the list
    model <- grade_models[[i]]
    
    # Generate predictions on grade_valid 
    pred <- predict(object = model,
                    newdata = grade_valid)
    
    # Compute validation RMSE and add to the 
    rmse_values[i] <- rmse(actual = grade_valid$final_grade, 
                           predicted = pred)
}

# Identify the model with smallest validation set RMSE
best_model <- grade_models[[which.min(rmse_values)]]
best_model
# Print the model paramters of the best model
best_model$control

# Compute test set RMSE on best_model
pred <- predict(object = best_model,
                newdata = grade_test)
rmse(actual = grade_test$final_grade, 
     predicted = pred)
	 
```
### Bagging - Bootstrap Aggregating

Sampling with replacement
some rows are represented multiple times and some are ignored
step 1 - pick b samples
common choice n/2
bootstrapped sample
collective knowledge of different people is greater than a single person
library(ipred)
Adv-
1) Increases the accuracy of resulting predictions
2) Reduces variance by averaging a set of observations

You'll be using the bagging() function from the ipred package. The number of bagged trees can be specified using the nbagg parameter, but here we will use the default (25).

If we want to estimate the model's accuracy using the "out-of-bag" (OOB) samples, we can set the the coob parameter to TRUE. The OOB samples are the training obsevations that were not selected into the bootstrapped sample (used in training). Since these observations were not used in training, we can use them instead to evaluate the accuracy of the model (done automatically inside the bagging() function).

- Receiver Operating Characteristic  useful tool for selectingmodel
AUC range 0-1
auc -1 perfectly classifies model

```
# Bagging is a randomized model, so let's set a seed (123) for reproducibility
set.seed(123)

# Train a bagged model
credit_model <- bagging(formula = default ~ ., 
                        data = credit_train,
                        coob = TRUE)

# Print the model
print(credit_model)
# Generate predicted classes using the model object
class_prediction <- predict(object = credit_model, 
                            newdata = credit_test,  
                            type = "class")         # return classification labels
# Print the predicted classes
print(class_prediction)
                            
# Calculate the confusion matrix for the test set
confusionMatrix(data = class_prediction,         
                reference = credit_test$default)  
# Generate predictions on the test set
pred <- predict(object = credit_model,
                newdata = credit_test,
                type = "prob")

# `pred` is a matrix
class(pred)
                
# Look at the pred format
head(pred)
                
# Compute the AUC (`actual` must be a binary (or 1/0 numeric) vector)
auc(actual = ifelse(credit_test$default == "yes", 1, 0), 
    predicted = pred[,"yes"])                    

# Specify the training configuration
ctrl <- trainControl(method = "cv",     # Cross-validation
                     number = 5,        # 5 folds
                     classProbs = TRUE,                  # For AUC
                     summaryFunction = twoClassSummary)  # For AUC

# Cross validate the credit model using "treebag" method; 
# Track AUC (Area under the ROC curve)
set.seed(1)  # for reproducibility
credit_caret_model <- train(default ~ ., 
                            data = credit_train, 
                            method = "treebag",
                            metric = "ROC",
                            trControl = ctrl)
                      
# Look at the model object
print(credit_caret_model)

# Inspect the contents of the model list 
names(credit_caret_model)

# Print the CV AUC
credit_caret_model$results[,"ROC"]

# Generate predictions on the test set
pred <- predict(object = credit_caret_model, 
                newdata = credit_test,
                type = "prob")

# Compute the AUC (`actual` must be a binary (or 1/0 numeric) vector)
auc(actual = ifelse(credit_test$default == "yes", 1, 0), 
                    predicted = pred[,"yes"])
					
# Print ipred::bagging test set AUC estimate
print(credit_ipred_model_test_auc)

# Print caret "treebag" test set AUC estimate
print(credit_caret_model_test_auc)
                
# Compare to caret 5-fold cross-validated AUC
credit_caret_model$results[,"ROC"]
```
