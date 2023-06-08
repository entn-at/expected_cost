# Expected cost

Methods for computing the expected cost (EC) on an evaluation dataset, as defined in statistical learning text books (e.g., Bishop's "Pattern recognition and machine learning", and Hastie's et al "The elements of statistical learning"). 
Given a matrix of user-defined costs with elements $c_{y\ d}$, where $y$ is the true class of a sample and $d$ is the decision made by the system for that sample, 
this metric is estimated as the average of the costs across all samples in the dataset. That is:

$EC = \frac{1}{K} \sum_k c_{y_k\ d_k}$

where the sum runs over the $K$ samples in the evaluation set and $c_{y_k\ d_k}$ is the cost incurred at sample $k$.

The EC is a generalization of the total error (which, in turn, is 1 minus the accuracy) and the balanced total error (which is 1 minus the balanced accuracy). The generalization is in the following ways: (1) it allows for costs that are different for each type of error, and (2) it allows for decisions that do not correspond one to one to the classes (e.g., it allows for the introduction of an "abstain" decision). The EC comes with an elegant theory on how to make optimal decisions given a certain set of costs, and it enables analysis of calibration. For these reasons we believe it is superior to other commonly used classification metrics, like the F-beta score or the Mathews correlation coefficient. All these issues are discussed in detail in:

*L. Ferrer, ["Analysis and Comparison of Classification Metrics"](https://arxiv.org/abs/2209.05355), 	arXiv:2209.05355*

The results in the paper can be replicated with the code in the examples directory in this repository.

The code provides methods for computing the EC when decisions are given by:

* hard decisions obtained with some external method, 

* Bayes decisions made by optimizing the cost given the scores from a system assuming they can be used to obtain well-calibrated posteriors, or

* optimal decisions made by choosing the decision threshold that minimizes the cost. This last option is only applicable for the binary case and the standard square cost function.

The scripts in the examples directory can be used with any dataset of scores and targets. See the examples/data.py file for examples on how to load your own data in the format required by the examples.

The repository provides calibration functionality using a separate repository called psr-calibration. The psr-calibration repository (which requires pytorch) is not needed for normal functioning of the code. A wrapper of the psr-calibration main calibration method can be found in the expected_cost/calibration.py file. An example on how to use this method can be found in the notebooks/data.py file. 

## How to install

1. Clone this repository:  

   ```git clone https://github.com/luferrer/expected_cost.git```

2. Install the requirements:  
   
   ```pip install -r requirements.txt```
   
3. (Optional) If you want to enable calibration capabilities follow the installation instructions in:

   [```https://github.com/luferrer/psr-calibration```](https://github.com/luferrer/psr-calibration)
  
   and link the psrcal directory from that repository in the expected_cost directory.
  
4. Run the example code in the examples dir. See the README in that dir for how to run the scripts.

