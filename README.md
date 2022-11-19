# Classification-of-precursor-microRNAs-in-various-groups-of-organisms
Objective:
To analyze the variations of different parameters used in creation of ML methods for pre-miRNA prediction, in various classes of organisms.

Data Collection:
We collected important data of Insects, Aves, Amphibia, Mammalia, Reptilia ,Rumins, Rice and Humans.
There are 502 data points for Mammalia, 910 for Rice, 1580 for Rodents, 1064 for Rumins, 606 for Sauria, 3855 for Insects, 1381 for Aves and 1916 for human. Total 11814 data points. We split the dataset into two parts train and test. 10% data is used for testing and 90% is used for training.
To overcome the problem of unbalanced dataset, as we see that Mammalia has 502 data points and Insects has 3855 data points, SMOTE was used. Synthetic Minority Oversampling Technique (SMOTE) is a statistical technique for increasing the number of data points in a dataset  to balance the groups (classes). It works by generating new instances from the minority classes.

Feature Engineering:
Principal Component Analysis (PCA) was used to extract meaningful features. It is a technique used in dimension reduction. It is an orthogonal linear transformation that transforms the data to a new coordinate system and extract the ones that has highest variance. These features can be useful to predict the classes. We extract 20 new features using PCA.
Parameter Optimization:
We used XGBoost model for prediction. XGBoost stands for Extreme Gradient Boosting. It is based on boosting algorithm, that attempts to build a strong classifier from the number of weak classifiers. Firstly, a model is built from training data and then second model tries to correct the errors present in the first model. There are various parameters used to tune XGBoost 
lambda: L2 regularization helps to reduce overfitting, ranges from 1e-3 to 10
alpha: L1 regularization helps to reduce overfitting, ranges from 1e-2 to 10.
colsample_bytree: Subsample ratio of columns when construction each tree, ranges from 0.3 to 1.0
subsample: Ratio of training instances, ranges from 0.2 to 1
learning_rate: Step size at each iteration while moving towards minimum of loss function, ranges from 0.001 to 0.1
n_estimators: Number of trees, ranges from 100 to 400 
max_depth: Max depth of a tree, ranges from 5 to 17
min_child_weight: Minimum instances needed to be in each node, ranges from 1 to 300

Performance Evaluation:
As there are more than 2 classes accuracy is not helpful how the good the model is. The metrics used are Sensitivity (SN), Specificity (SP), Accuracy (Acc), Precision (P), Recall (R), F1_score (F1) and Matthew’s correlation coefficient (MCC).
SN = TP/(TP+FN)
SP = TN/(TN+FP)
Acc = (TP+TN)/(TN+TP+FN+FP)
P = TP/(TP+FP)
F1 = 2×(SN×P)/(SN+P)
MCC = ((TP×TN)+(FP×FN))/√((TP+FP)×(TP+FN)×(TN+FP)×(TN+FN) )
where TP, FP, TN and FN are True Positive, False Positive, True Negative and False Negative respectively.


Results and Discussion:

Data Preparation and pre-processing:
There are total of 111 features used in prediction of classes
61 from dataset - 'Len', 'A', 'C', 'G', 'U', 'G+C', 'A+U', 'AA', 'AC', 'AG', 'AU', 'CA', 'CC', 'CG', 'CU', 'GA', 'GC', 'GG', 'GU', 'UA', 'UC', 'UG', 'UU', '%A', '%C', '%G', '%U', '%G+C', '%A+U', '%AA', '%AC', '%AG', '%AU', '%CA', '%CC', '%CG', '%CU', '%GA', '%GC', '%GG', '%GU', '%UA', '%UC', '%UG', '%UU', 'pb', 'Npb', 'mfe', 'dG', 'Q', 'NQ', 'D', 'ND', 'nstem', 'MFE1', 'MFE2', 'MFE3', 'MFE4', 'total_base', 'n_stems', 'avg_bp', 'SEQ'.
20 from PCA


Parameter Optimization:
Works best when n_estimators are between 100 to 400. Above 400 and below 100 accuracy drops. Similarly, for max_depth works best between 5 to 17. 
As the n_estimators and max_depth is increasing time taken by model to run is increasing, gpu_hist is used to make it run faster.
tree_method is used to enable GPUs as it runs faster than CPUs 
random_state is randomness of model while assigning weights initially.

