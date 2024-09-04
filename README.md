<H3>Enter Name:Yuvabharathi.B
<H3>Enter Register No:212222230181
<H3>Experiment -2
<H3>Date:
<h1 align =center>Implementation of Exact Inference Method of Bayesian Network</h1>

## Aim:
To implement the inference Burglary P(B| j,⥗m) in alarm problem by using Variable Elimination method in Python.

## Algorithm:

Step 1: Define the Bayesian Network structure for alarm problem with 5 random variables, Burglary,Earthquake,John Call,Mary Call and Alarm.<br>
Step 2: Define the Conditional Probability Distributions (CPDs) for each variable using the TabularCPD class from the pgmpy library.<br>
Step 3: Add the CPDs to the network.<br>
Step 4: Initialize the inference engine using the VariableElimination class from the pgmpy library.<br>
Step 5: Define the evidence (observed variables) and query variables.<br>
Step 6: Perform exact inference using the defined evidence and query variables.<br>
Step 7: Print the results.<br>

## Program :
## Import the Librareies
```
<from pgmpy.models import BayesianNetwork
from pgmpy.factors.discrete import TabularCPD
from pgmpy.inference import VariableElimination
```
## Define the network structure
```
network = BayesianNetwork([('Burglary', 'Alarm'),
                           ('Earthquake', 'Alarm'),
                           ('Alarm', 'JohnCalls'),
                           ('Alarm', 'MaryCalls')])
```
## Define the Conditional Probability Distributions (CPDs)
```
cpd_burglary = TabularCPD(variable='Burglary', variable_card=2, values=[[0.999], [0.001]])
cpd_earthquake = TabularCPD(variable='Earthquake', variable_card=2, values=[[0.998], [0.002]])
cpd_alarm = TabularCPD(variable='Alarm', variable_card=2,
                       values=[[0.999, 0.71, 0.06, 0.05],
                               [0.001, 0.29, 0.94, 0.95]],evidence=['Burglary', 'Earthquake'],evidence_card=[2, 2])
cpd_john_calls = TabularCPD(variable='JohnCalls', variable_card=2,
                             values=[[0.95, 0.1],
                                     [0.05, 0.9]],evidence=['Alarm'],evidence_card=[2])
cpd_mary_calls = TabularCPD(variable='MaryCalls', variable_card=2,
                             values=[[0.99, 0.01],
                                     [0.01, 0.99]], evidence=['Alarm'], evidence_card=[2])
```
## Add CPDs to the network
```
network.add_cpds(cpd_burglary, cpd_earthquake, cpd_alarm, cpd_john_calls, cpd_mary_calls)
```
## Initializethe inference
```
inference = VariableElimination(network)
```
## Perform inference
```
evidence = {'JohnCalls': 1, 'MaryCalls': 0}  # John called (1) and Mary didn't call (0) as evidence
query_variable = 'Burglary'
```
## Print the final value
```
result = inference.query(variables=[query_variable], evidence=evidence)
print(result)>
```



## Output :
![image](https://github.com/swathi22003343/Ex2---AAI/assets/120440439/8c5c7a3b-ae78-4efb-b172-3f039abdc3fb)


## Result :
Thus, Bayesian Inference was successfully determined using Variable Elimination Method
