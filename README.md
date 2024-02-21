**Table of Contents**

- [missLASSO](#missLASSO)
- [DOWNLOAD AND INSTALLATION](#download-and-installation)
- [Arguments](#Arguments)
- [Dataset](#Dataset)
- [Result](#Result)
- [Contact](#Contact)
- [Reference](#Reference)

# missLASSO 
`missLASSO` is a C++ software package that performs variable selection and estimation for the regression analysis of an outcome of interest against multiple types of features with missing data. We use a latent factor model to characterize the relationships across and within different types of features and to infer missing values from the observed data. Variable selection and estimation are performed by a penalized maximum likelihood approach and the estimator is computed using an EM algorithm.

# DOWNLOAD AND INSTALLATION
## Download
The latest version of missLASSO can be downloaded from [github page](https://github.com/alexwky/missLASSO).

## Installation
`missLASSO` is an executable file. Users can run it on the Linux or Window environment using `missLASSO.tar.gz` or `missLASSO.exe`, respectively.
### Linux Environment
1. Download `missLASSO.tar.gz` to a destinated directory
2. Go to the destinated directory:
    ```
    cd ./[destinated directory]
    ```
3. Extract `missLASSO.tar.gz`
    ```
    tar -xzvf missLASSO.tar.gz
    ```
4. Run `missLASSO` 
    ```
    ./missLASSO [type] [method] [penaltyno] [sizeX] [r] [groupsize] [cv] [lambda] [dirname] [foldername] [filename]
    Example : C:\Users\Desktop\missLASSO>missLASSO type 0 method 1 penaltyno 0 sizeX 0 r 1,1,1 groupsize 50,50 cv 1 lambda TestLambda.csv foldername testing filename SampleDataset_1.csv 
    ```
### Window Environment
1. Download `missLASSO.exe` to a destinated directory
2. Open command prompt and set the working directory
    ```
    cd ./[destinated directory]
    ```
3. Run `missLASSO`
    ```
    missLASSO [type] [method] [penaltyno] [sizeX] [r] [groupsize] [cv] [lambda] [dirname] [foldername] [filename]
    Example : C:\Users\Desktop\missLASSO>missLASSO type 0 method 1 penaltyno 0 sizeX 0 r 1,1,1,1 groupsize 30,30,30 cv 1 lambda TestLambda.csv foldername testing filename SampleDataset.csv 
    ```

# Input

There are 13 arguments for the function:

| Argument | Description | Value(s) / Format | Interpretation | Can be Omitted | Remark |
| --------- | --- | ---- | ---- | --- | ---- |
| type  | Type of the outcome variable | 0/1  |<ul><li>0: Gaussian</li><li>1: Binary</li></ul>  | ✖  | -  |
| method | Method for handling missing data | 0/1  |<ul><li>0: Complete case analysis </li><li>1: Single imputation and the full likelihood approach</li></ul>  | ✖  | -  |
| penaltyno | Penalty type| 0/1  | <ul><li>0: Lasso </li><li>1: Adaptive lasso with marginal coefficients as weights </li></ul>  | ✖  | -  |
| sizeX  | Number of covariates (not modeled by the factor model) | Integer ≥ 0  || ✖  | - |
| r  | Numbers of latent factors for different types of features |   | -  | ✖  | seperate using ","; the first component is the number of common factors, and the later components correspond to the number of factors specific to a type  |
| groupsize  | Number of variables for each type of features  | | - | ✖  | seperate using ","  |
| cv  |Cross validation|0/1 |<ul><li>0: Do not perform cross validation </li><li>1: Perform cross validation</li> | ✔  | default is to perform cross validation  |
| lambda  | sequence of tuning parameter values | .csv file | - | ✔ | -  |
| XyExclude  | Indices of covariates that are to be excluded from the outcome model |  | - | ✔ | separated using ","; by default, all covariates are included |
| XsExclude  | Indices of covariates that are to be excluded from the factor model |  | - | ✔ | separated using ","; by default, all covariates are included |
| dirname  | Output directory | Any file path | -  | ✔  | <ul><li>Relative path can be used</li><li>Default: current working directory</li></ul>  |
| foldername  | Output folder name | Any name | -  | ✔  | Default is `Result`  |
| filename  | Input dataset name | .csv file | -  | ✖  | - |


# Dataset

The input dataset should be in `.csv` format and consist of 3 sets of input: outcome `Y`, covariates `X`, and potentially missing covariates `S`. The dataset is in the format of a `n x (p+k+1)`-matrix, where `n` is the sample size, `p` is the number of covariates, and `k` is the number of potentially missing covariates. The dataset should be in following format:
|Outcome variable| 1st covariate |2nd covariate|...|pth covariate|1st missing covariate|2nd missing covariate|...|kth missing covariate|
|---|---|---|---|---|---|---|---|---|
||||||||||

A sample dataset can be downloaded from [github page](https://github.com/alexwky/missLASSO).

`SampleDataset_1.csv` is a dataset without covariate `X` and contains potentially missing covariate `S` only, with groupsize = 50,50.

`SampleDataset_2.csv` is a dataset with covariate `X` and potentially missing covariate `S`, with sizeX = 6,  groupsize = 50,50,50.

# Output

All results will be stored in an output folder. By default, the output folder is called "Result" under the current working directory. The output folder will contain the following `.csv` files:

`Complete case analysis` (method = 0)
 1. Complete.csv
 2. Complete-lambda.csv
 3. Complete-loglikelihood.csv
 
`Single imputation and full likelihood approach` (method = 1)
 1. Impute.csv
 2. Impute-imploglikelihood.csv
 3. Impute-lambda.csv
 4. Impute-loglikelihood.csv
 5. Impute-param.csv
 6. Joint.csv
 7. Joint-lambda.csv
 8. Joint-loglikelihood.csv
 9. Joint-param.csv

The descriptions of the output files are as follows:

| File | Description |
| --------- | --- |
| Complete.csv/Impute.csv/Joint.csv  | Regression coefficients in the outcome model over all tuning parameter values considered. Let `q` be the number of tuning parameter values. The first `q` components of the output correspond to the numbers of nonzero coefficients under the tuning parameter values. Let `m` be the sum of the first `q` components of the output. The `q+1`-th to the `q+m`-th components correspond to the positions of the nonzero coefficients. The `q+m+1`-th to the `q+2m`-th components correspond to the values of the nonzero coefficients. For example, if `q=3` and the output is `1,2,4,0,0,1,0,1,2,3,0.3,0.3,0.4,0.4,0.5,0.6,0.7`, then for the first tuning parameter value, one variable is selected, the position is 0 (i.e., the first variable), and the coefficient is 0.3; for the second tuning parameter value, two variables are selected, the positions are (0,1), and the coefficients are (0.3,0.4); for the third tuning parameter, four variables are selected, the positions are (0,1,2,3), and the coefficients are (0.4,0.5,0.6,0.7). |
| Complete-lambda.csv/Impute-lambda.csv/Joint-lambda.csv  | Sequence of lambda values considered. If cv=1, then the last component of the lambda sequence is that selected by cross validation.|
| Complete-loglikelihood.csv/Impute-loglikelihood.csv/Joint-loglikelihood.csv  |Sequence of log-likelihood values, corresponding to the lambda values in the "-lambda.csv" files |
| Impute-imploglikelihood.csv | loglikelihood value evaluated at the imputed data|
| Joint-param.csv | All parameter estimates at the selected tuning parameter value. The parameter estimates are ordered as follows: $\beta$, $\alpha$, $\Gamma$ (intercept), $\Gamma$ (coefficients of covariates), $\Psi$, $\Sigma$ (diagonal elements), $\xi$ (error variance for the linear outcome model); refer to Wong et al. (2023) for the parameter names. |

# Contact

Wong Kin Yau, Alex <<kin-yau.wong@polyu.edu.hk>>

# Reference #

Wong, K. Y., Zeng, D., and Lin, D. Y. (2023), "Penalized regression for multiple types of many features with missing data," Statistica Sinica, 33, 633–662.


