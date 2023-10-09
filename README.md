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
1. Download `missLASSO.exe` to a destionated directory
2. Open command prompt and set the working directory
    ```
    cd ./[destinated directory]
    ```
3. Run `missLASSO`
    ```
    missLASSO [type] [method] [penaltyno] [sizeX] [r] [groupsize] [cv] [lambda] [dirname] [foldername] [filename]
    Example : C:\Users\Desktop\missLASSO>missLASSO type 0 method 1 penaltyno 0 sizeX 0 r 1,1,1,1 groupsize 30,30,30 cv 1 lambda TestLambda.csv foldername testing filename SampleDataset.csv 
    ```

# Arguments

There are 13 arguments for the function:

| Argument | Description | Value(s) / Format | Meanings | Omit | Remark |
| --------- | --- | ---- | ---- | --- | ---- |
| type  | Type of the outcome variable | 0/1  |<ul><li>0 : Gaussian</li><li>1: Binary</li></ul>  | ✖  | -  |
| method | Method for handling missing data | 0/1  |<ul><li>0 : Complete case analysis </li><li>1: Single imputation and full likelihood approach</li></ul>  | ✖  | -  |
| penaltyno | Penalty type| 0/1  | <ul><li>0 : Lasso </li><li>1: Adaptive lasso with marginal coefficient as weight </li></ul>  | ✖  | -  |
| sizeX  | Number of covariates (not modeled by the factor model) | Integer ≥ 0  || ✖  | - |
| r  | Numbers of latent variables for each type of features |   | -  | ✖  | seperate using ","; the first component is the number of common factors, and the later components correspond to the number of factors specific to a type  |
| groupsize  |Dimension of each latent variables  | | - | ✖  | seperate using ","  |
| cv  |Cross-Validation|0/1 |<ul><li>0 : Don't do Cross-Validation </li><li>1: Do Cross-Validation</li> | ✔  | -  |
| lambda  |lambda series | .csv file | - | ✔ | -  |
| XyExclude  |The column number(s) to exclude from the covariates of Y |  | - | ✔ | By default, all X are included |
| XsExclude  |The column number(s) to exclude from the covariates of X  |  | - | ✔ | By default, all X are included |
| dirname  | Output directory | Any file path | -  | ✔  | <ul><li>Relative path can be used</li><li>Default : current working directory</li></ul>  |
| foldername  | Output folder name | Any name | -  | ✔  | Default `Result`  |
| filename  | Input dataset name | .csv file | -  | ✖  | - |


# Dataset

The input dataset should be in `.csv` format and consist of 3 components outcome variable `Y`, covariates `X` and potentially missing covariates `S`. Therefore, dataset is a `n x (p+k+1)` amatrix, where `n` is the sample size, `p` is the number of covariates and `k` is the number of potentially missing covariates. The dataset should be in following format:
|Outcome variable| 1st covariate |2nd covariate|...|pth covariate|1st missing covariate|2nd missing covariate|...|kth missing covariate|
|---|---|---|---|---|---|---|---|---|
||||||||||

*Sample dataset can be downloaded from [github page](https://github.com/alexwky/LASSO).

`SampleDataset_1.csv` is a dataset without covariate `X` and contain potentially covariate `S` only, with groupsize = 50,50 and r = 1,1,1.

`SampleDataset_2.csv` is a dataset with both covariate `X` and contain potentially covariate `S` only, with sizeX = 6,  groupsize = 50,50,50 and r = 1,1,1,1.

# Result

The results will be stored in an output folder. By default, the output folder is called "Result" under current working directory. The output folder consist of following `.csv` files:

`Complete mode` (mode == 0)
 1. Complete.csv
 2. Completye-lambda.csv
 3. Complete-loglikelihood.csv
 
`Impute & Joint mode` (mode == 1)
 1. Impute.csv
 2. Impute-imploglikelihood.csv
 3. Impute-lambda.csv
 4. Impute-loglikelihood.csv
 5. Impute-param.csv
 6. Joint.csv
 7. Joint-lambda.csv
 8. Joint-loglikelihood.csv
 9. Joint-param.csv

# Contact

Wong Kin Yau, Alex <<kin-yau.wong@polyu.edu.hk>>

# Reference #

Wong, K. Y., Zeng, D., and Lin, D. Y. (2023), "Penalized regression for multiple types of many features with missing data," Statistica Sinica, 33, 633–662.


