# Random Forest

<script src="../js/general.js"></script>

###Discussion and flows
---

Random Forest is a **divide-and-conquer** method useful for data classification and 
regression. Random Forest is an **ensemble learning** method - generate several classifiers and 
aggregate their results into one at final - built on **decision trees** (figure.1 [1]). In the other 
words, a model generated by random forest combines several weaker learners (classifiers) into 
a stronger learner at final. The following figure.2 [1] is an example of the above statements. 

![](../images/rf_decision-tree.png)

[Figure.1] A simple example demonstrates decision trees. There is a variable with conditions to classify two dimension data, people who want to play and not to play ball games. 

![](../images/rf_random_forest.png)

[Figure.2] The basic concept implements random forest method. The blue point represents each observed data. Each gray curve, a weaker learner, is an approximation to one subset of total data. The red curve, a stronger learner, is much better and outstanding than the other gray curve. 