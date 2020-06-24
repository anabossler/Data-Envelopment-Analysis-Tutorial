# Data Envelopment Analysis(DEA) Tutorial

## Table of Contents
[TOC]

## Introduction
### Background and Motivation
Efficiency considers the relationship between input and output which under the same input, the higher the output, the higher the efficiency. Therefore, evaluating  efficiency is a crucial factor in managing a company for production. In practically production, the true production function is almost impossible to be observed. However, if we don't have the production function, then the efficiency can't be evaluted. Consequently, it must to be propose an approach to estimate the production function for evaluating efficiency.

### What is DEA?
DEA is a methodology based on benchmarking techniques, and also a non-paramistics approach by estimating production function from existing data for evaluating the efficiency of comparable entities (Decision making units (DMUs))^[5]^.

### Why use DEA?
In practically, production usually is a system of Multi-Input Multi-Output(MIMO) which is almost impossible to formulate even guess the true production function because it has a high dimension of data. DEA is a nonparamic approach which have the benefit of not require to assuming a particular functional shape for the frontier, however it estimating approximately production function with existing data.^[2]^.

### Constraints of DEA
* The input and output data must be very clear, therefore it can't be  the dummy variable or categorical variable, or the evaluation will be biased. 
* Between the evaluated DMUs are required have "Homogeneity", that is,  the different nature or different scale is not advisable to compare the various DMUs of each other.
* The result evaluated by DEA is the relative efficiency among the DMUs, not the absolute efficiency, therefore, it is not appropriate to use the estimated "relative efficiency" as an absolute value.
* DEA is extremely sensitive to noise of data, therefore, the data to be evaluated should be as correct as possible.

## Prerequisite knowledge
### Production function
A production function stands for a production frontier which also represents a "maximum outputs" that can be achieved using input vector 𝕩. In addition, the data resource as must come from the same industry as possible because the different industry may have different  resource consumption proportion and quantity of outputs for technique.
![Illustration of Production function](https://i.imgur.com/eCINgfv.png)

#### **Properties of Production function^[1]^**
* **Nonnegativity:** The production output is a finite, non-negative, real number.
* **Weak Essentiality:** The production output cannot be generated without the use of at least one input.
* **Monotonicity:** Additional units of an input will not decrease output; also called nondecreasing in 𝕩.
* **Concavity:** Any linear combination of the vectors $𝕩^0$ and $𝕩^1$ will produce an output that is no less than the same linear combination of $f(𝕩^0)$ and $f(𝕩^1)$. That is ,$f(𝜆𝕩^0+(1-𝜆)𝕩^1\geq𝜆f(𝕩^0)+(1-𝜆)f(𝕩^1)$. This property implies the "law of diminishing marginal returns".

#### **Exception**
Above properties are not very exhaustive, nor are universally maintained. 
* Monotonicity is relaxed when the input congestion. e.g. Purchasing more machines will increase productivity, but too many machines will reduce the productivity of the machine due to other external factors
* Concavity is relaxed to characterize an S-shaped production function^[5]^
![](https://i.imgur.com/ikuMIwE.png)


### Variable Returns to Scale
In production(economics), returns to scale describe how change to long run returns as the scale of production increases, when all input levels are variable. The concept of returns to scale arises from a production function of company which explains the linkage of the rate of increase in output (production) relative to associated increases in input (factors of production). In the long run, all factors of production are variable and subject to change in response to a given increase in production scale^[4]^. 
![](https://i.imgur.com/C9nLYTw.png)
#### **There are three possible types of returns to scale：**
*  **Constant returns to scale(CRS)**
The quantity of increase for output is proportional to the input when it increase the input.
**# Conclusion：** This is a optimal state for production of company.

*  **Decreasing  returns to scale(DRS)**
The quantity of increase for output is less than the input when it increase the input.
**# Conclusion：** This state implies that the company is under the too large production scale which is not recommended to increase more input.

*  **Increasing  returns to scale(IRS)**
The quantity of increase for output is larger than the input when it increase the input.
**# Conclusion：** This state implies that the company is under the too large production scale which is recommended to increase more input.

#### **Comparison**
###### Mathematical illustration of three properties where $𝜆>1.$
| Return to Scale | Mathematical Formulation |
|:---------------:|:------------------------:|
|       DRS       |      $𝑓(𝜆𝕩)<𝜆𝑓(𝕩)$       |
|       CRS       |      $𝑓(𝜆𝕩)=𝜆𝑓(𝕩)$       |
|       IRS       |      $𝑓(𝜆𝕩)>𝜆𝑓(𝕩)$       |


## How do DEA model work?
### DEA model
#### **Notation**
##### Set：
* $K$：It is the set of Decision-Making Units(DMUs).
* $I$：It is the set of all inputs.
* $J$：It is the set of all outputs.
##### Index：
* $k, r$：These are the index of set $K$ and $r$ is refer to a specific firm in set $K$ ($k, r \in K$).
* $i$：It is an index of the set $I$ ($i \in I$).
* $j$：It is an index of the set $J$ ($j \in J$).
##### Decision variables：
* $θ_{r}$：It is the dual variable of the $r^{th}$ DMUs.
* $λ_{k}$：It is the dual variable of the $k^{th}$ DMUs.
* $v_{ki}$ It is the $i^{th}$ variables of the $k^{th}$ weights of input data.
* $u_{kj}$ It is the $j^{th}$ variables of the $k^{th}$ weights of output data. 

##### Parameters：
* $X_{ri}, X_{ki}$：These are the $i^{th}$ input data of the $k^{th}$ or $r^{th}$ DMUs.
* $Y_{rj}, Y_{kj}$：These are the $j^{th}$ output data of the $k^{th}$ or $r^{th}$ DMUs.


### CRS DEA model
#### **History：**
Based on Ferrell's  model of measuring efficiency, Charnes, Cooper, and Rhodes (CCR) propose the CRS DEA model in 1978 which is also called CCR model.
#### **Goal:** 
Measure **"Overall Efficiency (OE)"** and identify the **"Most Productive Scale Size(MPSS)"** of **"one specific firm r"**.
#### **Primal Formulation：**
This is a Fractional Programming！
$$
Max\ E_{r}^{CRS}=\frac{\sum_{j=1}^{J}u_{rj}Y_{rj}}{\sum_{i=1}^{I}v_{ri}X_{ri}}
$$

\begin{align}
s.t. &\frac{\sum_{j=1}^{J}u_{rj}Y_{kj}}{\sum_{i=1}^{I}v_{ri}X_{ki}} \leq 1, ∀𝑘 \\
&u_{rj}\geq0, ∀j \\
&v_{ri}\geq0, ∀i
\end{align}

##### This formulation has
— $I+J$ decision variables
— $1+K+I+J$ constraints

#### **Dual Formulation：**
Because primal formulation is a fractional programming which is also a nonlinear programming , therefore primal formulation can be transformed to dual formulation by dual  theory for simplizing the caculation. 
$$
Min\ E_{r}^{CRS}=𝜃_{r}
$$

\begin{align}
s.t. &\sum_{k=1}^{K}𝜆_{k}X_{ki}\leq𝜃_{r}X_{ri}, ∀i \\
&\sum_{k=1}^{K}𝜆_{k}Y_{kj}\geq  Y_{rj}, ∀j \\
&𝜆_{k}\geq0, ∀k
\end{align}

##### This formulation has
— $K$ decision variables
— $K+I+J$ constraints


### VRS DEA model
#### **History：**
Banker, Charnes, and Cooper (BCC) relaxed the assumption of constant returns to scale who propose VRS DEA model in 1984 which is also called BCC model.
#### **Goal:** 
Measure **"Technical Efficiency (TE)"** of **"one specific firm r"**.

#### **Primal Formulation：**
$$
Max\ E_{r}^{VRS}=\frac{\sum_{j=1}^{J}u_{rj}Y_{rj}-u_{0r}}{\sum_{i=1}^{I}v_{ri}X_{ri}}
$$

\begin{align}
s.t. &\frac{\sum_{j=1}^{J}u_{rj}Y_{kj}-u_{0r}}{\sum_{i=1}^{I}v_{ri}X_{ki}} \leq 1, ∀𝑘 \\
&u_{rj}\geq0, ∀j \\
&v_{ri}\geq0, ∀i \\
&u_{0r}\ \mathrm{is\ free\ variable}
\end{align}


#### **Dual Formulation：** 
$$
Min\ E_{r}^{VRS}=𝜃_{r}
$$

\begin{align}
s.t. &\sum_{k=1}^{K}𝜆_{k}X_{ki}\leq𝜃_{r}X_{ri}, ∀i \\
&\sum_{k=1}^{K}𝜆_{k}Y_{kj}\geq  Y_{rj}, ∀j \\
&\sum_{k=1}^{K}𝜆_{k}=1 \\
&𝜆_{k}\geq0, ∀k
\end{align}

## How to evaluate the efficiency?
### Input-Oriented Model 
As shown below, the point of $r$ is the current state of input and the point of $r'$ is the optimal state of the input. Accordingly, The idea of input-oriented model is to "proportionally reduce the quantities of input without changing the quantities output".
![](https://i.imgur.com/NtW5TrW.png)

### Output-Oriented Model
As shown below, the point of $r$ is the current state of output and the point of $r'$ is the optimal state of the output. Accordingly, The idea of output-oriented model is to "proportionally expand the quantities of output without altering the quantities input".
![](https://i.imgur.com/Cy1gylc.png)

### Decomposing the Overall Efficiency
#### **Component：**
* **Overall Efficiency(OE)** is the optimal solution($E_{r}^{CRS}$) of CRS DEA model.
* **Technical Efficiency(TE)** is the optimal solution($E_{r}^{VRS}$) of VRS DEA model.
* **Scale Efficiency (SE)** can be calculate by dividing the $OE$ by the $TE$. In addition, economic scale affects the productivity of a firm, then a firm would like to achieve "economic scale" to reduce the production cost.
#### Formulation：
$$
\mathrm{Overall\ efficiency(OE)=Technical\ efficiency(TE)\times Scale\ efficiency(SE)}
$$

### Illustration of efficiency decomposion
This is an input-oriented model for illustrating the components of efficiency.
![](https://i.imgur.com/vbxyyG8.png)
#### **Geometry Character：**
$$
OE=\frac{\overline{or*}}{\overline{or}},\quad 
TE=\frac{\overline{or'}}{\overline{or}},\quad
SE=\frac{\overline{or*}}{\overline{or'}}
$$ 

## Case study：Airline Efficiency
### Data preparation
In the case, there are 13 airlines(DMUs) to be estimated efficiency with three inputs and two outputs. The input data including Aircraft, Fuel and Employee and the output data including Passenger and Freight^[3]^.
| $$\mathrm{DMU}$$ | $$\mathrm{aircraft\\(fleet size)}$$ | $$\mathrm{Fuel\\(gallons)}$$ | $$\mathrm{Employee\\(units)}$$ | $$\mathrm{Passenger\\(passenger-miles)}$$ | $$\mathrm{Freight\\(ton-miles)}$$ |
| --- | -------- | ---- | -------- | --------- | ------- |
| A   | 109      | 392  | 8259     | 23756     | 870     |
| B   | 115      | 381  | 9628     | 24183     | 1359    |
| C   | 767      | 2673 | 70923    | 163483    | 12449   |
| D   | 90       | 282  | 9683     | 10370     | 509     |
| E   | 461      | 1608 | 40630    | 99047     | 3726    |
| F   | 628      | 2074 | 47420    | 128635    | 9214    |
| G   | 81       | 75   | 7115     | 11962     | 536     |
| H   | 153      | 458  | 10177    | 32436     | 1462    |
| I   | 455      | 1722 | 29124    | 83862     | 6337    |
| J   | 103      | 400  | 8987     | 14618     | 785     |
| K   | 547      | 1217 | 34680    | 99636     | 6597    |
| L   | 560      | 2532 | 51536    | 135480    | 10928   |
| M   | 423      | 1303 | 32683    | 74106     | 4258    |

### Environment
```
Python 3.7.4 + PuLP 2.0
```

### Execute
#### **Step. 1**
Import the essential package.
```python
import csv
from pulp import LpProblem, LpMinimize, LpVariable, lpSum, value
```
#### **Step. 2**
Build the sets.
```python
K = ["A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M"]
I = ["Aircraft", "Fuel", "Employee"]
J = ["Passenger", "Freight"]
```
#### **Step. 3**
Import the csv data. 
```python
X = { 
    i: {
        k: 0 for k in K
    } for i in I
}
Y = { 
    j: {
        k: 0 for k in K
    } for j in J
}
with open('airlines_data.csv', newline='') as csvfile:
    rows = csv.DictReader(csvfile)
    k = 0
    for row in rows:
        for i in I:
            X[i][K[k]] = float(row[i]) 
        for j in J:
            Y[j][K[k]] = float(row[j])
        k += 1
```

#### **Step. 4**
In this case, I use dual formulation and input-oriented model to implement the CRS DEA model.
* Building the model
```python
model = LpProblem('CRS_model', LpMinimize)
```
* Building the decision variables $𝜃_{r}$ and $𝜆_{k}$.
```python
theta_r = LpVariable(f'theta_r')
lambda_k = LpVariable.dicts(f'lambda_k', lowBound=0, indexs=K)
```
* Setting the objective function
$$
Min\ E_{r}^{CRS}=𝜃_{r}
$$
```python
model += theta_r #Dual formulation
```

* Setting the constraints
\begin{align}
s.t. &\sum_{k=1}^{K}𝜆_{k}X_{ki}\leq𝜃_{r}X_{ri}, ∀i \\
&\sum_{k=1}^{K}𝜆_{k}Y_{kj}\geq  Y_{rj}, ∀j
\end{align}
```python
for i in I:
    model += lpSum([
            lambda_k[k] * X[i][k]
        for k in K]) <= theta_r * float(X[i][K[r]])
for j in J:
    model += lpSum([
            lambda_k[k] * Y[j][k]
        for k in K]) >= float(Y[j][K[r]])
```

* Solving the model
```python
model.solve()
```

#### **Step. 5**
In this case, I use dual formulation and input-oriented model to implement the VRS DEA model.
* Building the model
```python
model = LpProblem('VRS_model', LpMinimize)
```
* Building the decision variables $𝜃_{r}$ and $𝜆_{k}$.
```python
theta_r = LpVariable(f'theta_r')
lambda_k = LpVariable.dicts(f'lambda_k', lowBound=0, indexs = K)
```
* Setting the objective function
$$
Min\ E_{r}^{VRS}=𝜃_{r}
$$
```python
model += theta_r #Dual formulation
```

* Setting the constraints
\begin{align}
s.t. &\sum_{k=1}^{K}𝜆_{k}X_{ki}\leq𝜃_{r}X_{ri}, ∀i \\
&\sum_{k=1}^{K}𝜆_{k}Y_{kj}\geq  Y_{rj}, ∀j \\
&\sum_{k=1}^{K}𝜆_{k}=1
\end{align}
```python
for i in I:
        model += lpSum([
                lambda_k[k] * X[i][k]
            for k in K]) <= theta_r * float(X[i][K[r]])
    for j in J:
        model += lpSum([
                lambda_k[k] * Y[j][k]
            for k in K]) >= float(Y[j][K[r]])
    model += lpSum([ lambda_k[k] for k in K]) == 1 #Convex Combination for r'
```

* Solving the model
```python
model.solve()
```

#### **Step. 6**
Call the function for output.
```python
OE_outputText = 'These are OE of all DMUs\n-------------\n'
TE_outputText = 'These are TE of all DMUs\n-------------\n'
SE_outputText = 'These are SE of all DMUs\n-------------\n'

for k in range(len(K)):
    OE_text, OE_val = getOverallEfficiency(k)
    TE_text, TE_val = getTechnicalEfficiency(k)
    OE_outputText += OE_text
    TE_outputText += TE_text
    SE_outputText += f'{K[k]}：{round(OE_val / TE_val, 3)}\n'
print(OE_outputText)
print(TE_outputText)
print(SE_outputText)
```

### Result
We found that DMUs of C, G, H, I, K and L are in a better efficiency state then the DMUs of D, J and M are in a poor efficiency state from this table, which suggest to the DMUs of D and J can decompose the SE with input and output data for understanding and improving the poor efficiency state.

| DMU | OE    | TE    | SE    |
| --- | ----- | ----- | ----- |
| A   | 0.978 | 1     | 0.978 |
| B   | 0.968 | 1     | 0.968 |
| C   | 1     | 1     | 1     |
| D   | 0.537 | 0.9   | 0.597 |
| E   | 0.969 | 0.996 | 0.973 |
| F   | 0.978 | 1     | 0.978 |
| G   | 1     | 1     | 1     |
| H   | 1     | 1     | 1     |
| I   | 1     | 1     | 1     |
| J   | 0.619 | 0.886 | 0.698 |
| K   | 1     | 1     | 1     |
| L   | 1     | 1     | 1     |
| M   | 0.835 | 0.849 | 0.984 |

## Comments
DEA is a robust technique for evaluating efficiency when I want to know that how to benchmark the different airlines or branches of the bank. This technique is suitable for executive or analyst in any industry that needs to evaluate the efficiency of homogeneous units , which especially in manufacturing. During apply the DEA model, the units can be compare each other by relative efficiency but it can't tell us how to improve the efficiency. As a result, it need to apply another apporch for finding out the solution of improvement because DEA just a tool for evaluating relative  efficiency of each units.



## Reference
[1] Coelli, T. J., Rao, D. S. P., O'Donnell, C. J., & Battese, G. E. (2005). An introduction to efficiency and productivity analysis. Springer Science & Business Media.
[2] Data envelopment analysis. (2020,June 9). In Wikipedia, the free encyclopedia. Retrieved June 20, 2020, from https://en.wikipedia.org/wiki/Data_envelopment_analysis
[3] Lee, C. Y., & Johnson, A. L. (2012). Two-dimensional efficiency decomposition to measure the demand effect in productivity analysis. European Journal of Operational Research, 216(3), 584-593.
[4] Returns to scale (2020, April 16). In Wikipedia, the free encyclopedia. Retrieved June 22, 2020, from https://en.wikipedia.org/wiki/Returns_to_scale
[5] Vörösmarty, G., & Dobos, I. (2020). A literature review of sustainable supplier evaluation with Data Envelopment Analysis. Journal of Cleaner Production, 121672.
