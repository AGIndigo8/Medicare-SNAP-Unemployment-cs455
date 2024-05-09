# An analysis of regional medical needs as a function of social welfare programs

This project analyzes data from three sources: SNAP enrollment, unemployment, and medicare charges.
The goals of the project involve finding patterns in the data to inform social policy decisions.
In particular, the prevelence of certain diseases is considered by the amount of charges seen for that class of treatment through medicare.
This is compared to SNAP enrollment, which is seen as the main parameter of interest in the policies that this analysis attempts to inform.
Unemployment is used as a proxy for economic wellbeing in the regions.

The analysis takes three phases, each contained in a notebook in this codebase.

* Phase 1 (Data Preperation): This phase uses Spark in a cluster of 10 machines to merge the datasets and conform them to useful features.
* Phase 2 (Linear Regression): This phase uses Spark to perform linear regression. This attempts to highlight specious correlations between particular diseases and (each) SNAP enrollment/unemployment. Diseases of interest are selected for further scrutiny.
* Phase 3 (Machine Learning): This phase attempts to predict the ideal SNAP enrollment levels for a region (as characterized by its unemployment) so as to minimize the medical charges associated with diseases of interest.
  This phase first trains random forest classifiers for each disease to predict the medicare charges associated with it as a function of SNAP enrollment and unemployment in that region. The accuracy of these to further determine which correlations are significant.
  Finally the SNAP feature of the random forest is replaced by an MLP. This MLP takes the unemployment as an input and outputs a predicted SNAP enrollment.
  This is trained in a self-supervised way to minimize the output of the random forest for given unemployment values and predicted snap values.
