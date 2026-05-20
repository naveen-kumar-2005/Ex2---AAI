<H3>Name: NAVEEN KUMAR R</H3>
<H3>Register No: 212223230139</H3>
<H3>Experiment: 2</H3>
<H3>Date: 12.05.2026</H3>
<h1 align =center>Implementation of Exact Inference Method of Bayesian Network</h1>

## Aim:
To implement the inference Burglary P(B| j,⥗m) in alarm problem by using Variable Elimination method in Python

## Algorithm:

<b>Step 1:</b> Define the Bayesian Network structure for alarm problem with 5 random variables, Burglary, Earthquake, John Call, Mary Call and Alarm

<b>Step 2:</b> Define the Conditional Probability Distributions (CPDs) for each variable using the TabularCPD class from the pgmpy library

<b>Step 3:</b> Add the CPDs to the network

<b>Step 4:</b> Initialize the inference engine using the VariableElimination class from the pgmpy library

<b>Step 5:</b> Define the evidence (observed variables) and query variables

<b>Step 6:</b> Perform exact inference using the defined evidence and query variables

<b>Step 7:</b> Print the results

## Program:
```python
# Import required libraries
from pgmpy.models import BayesianNetwork
from pgmpy.factors.discrete import TabularCPD
from pgmpy.inference import VariableElimination

# Define bayesian network structure
network=BayesianNetwork([
    ('Burglary','Alarm'),
    ('Earthquake','Alarm'),
    ('Alarm','JohnCalls'),
    ('Alarm','MaryCalls')
])

# Define the conditional probability distributions
cpd_burglary = TabularCPD(variable='Burglary',variable_card=2,values=[[0.999],[0.001]])
cpd_earthquake = TabularCPD(variable='Earthquake',variable_card=2,values=[[0.998],[0.002]])
cpd_alarm = TabularCPD(variable ='Alarm',variable_card=2, values=[[0.999, 0.71, 0.06, 0.05],[0.001, 0.29, 0.94, 0.95]],evidence=['Burglary','Earthquake'],evidence_card=[2,2])
cpd_john_calls = TabularCPD(variable='JohnCalls',variable_card=2,values=[[0.95,0.1],[0.05,0.9]],evidence=['Alarm'],evidence_card=[2])
cpd_mary_calls = TabularCPD(variable='MaryCalls',variable_card=2,values=[[0.99,0.3],[0.01,0.7]],evidence=['Alarm'],evidence_card=[2])

# Add CPDs to the network
network.add_cpds(cpd_burglary,cpd_earthquake,cpd_alarm,cpd_john_calls,cpd_mary_calls)

# Initialize the inference engine
inference = VariableElimination(network)

# Perform exact inference - 1
evidence = {'JohnCalls':1,'MaryCalls':0} # john called(1) and mary didn't call(0) as evidence
query_variable ='Burglary'
result = inference.query(variables=[query_variable],evidence=evidence)

# Print result - 1
print(result)

# Perform exact inference - 2
evidence1 ={'JohnCalls':1,'MaryCalls':1} # john called(1) and mary called(1) as evidence
query_variable ='Burglary'
result2 = inference.query(variables=[query_variable],evidence=evidence)

# Print result - 2
print(result2)
```

## Output:
<img width="347" height="312" alt="image" src="https://github.com/user-attachments/assets/89226f1c-bb7d-4f21-ba9b-c2b459c7be25" />

## Result:
Thus, Bayesian Inference was successfully determined using Variable Elimination Method
