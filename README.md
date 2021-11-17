**Table of Contents**

- [LASSO](#LASSO)
- [DOWNLOAD AND INSTALLATION](#download-and-installation)
- [Arguments](#Arguments)
- [Dataset](#Dataset)
- [Result](#Result)
- [Contact](#Contact)
- [Reference](#Reference)

# LASSO 
LASSO is a C++ software package that perform penalized-likelihood approach for multiple typee of many features with missing data using expectation-maximization (EM) algorithm. We use a latent variable model to characterize the relationships across and within data types and to infer missing values from observed data. We develop a penalized-likelihood approach for variable selection and parameter estimation and devise an efficient expectation-maximization (EM) algorithm to implement our approach. We establish the asymptotic properties of the proposed estimators when the number of features increases at a polynomial rate of the sample size. 

# DOWNLOAD AND INSTALLATION
## Download
The latest version of LASSO can be downloaded from [github page](https://github.com/alexwky/LASSO).

## Installation
LASSO is an executable file. Run `LASSO.exe` through command prompt with a vector of arguments and an organized dataset.
1. Go to the directory that have `LASSO.exe`
    ```
    cd ./[destination directory]
    ```
2. Run `LASSO.exe` 
    ```
    LASSO [type] [method] [penaltyno] [sizeX] [r] [groupsize] [dirname] [foldername]
    ```
3. `LASSO.exe` will ask for yuor dataset
    ```
    C:\Users\Desktop\LASSO>LASSO type 0 method 1 penaltyno 0 sizeX 0 r 1,1,1,1 groupsize 30,30,30
    please input the path of the dataset : [Input your dataset here]
    ```
    *You can input the relative path of the dataset if the dataset is not at the same directory of `LASSO.exe`
    

# Arguments

There are 8 arguments that users have to input to the executable file through command prompt. Please read the following table for the details of the 8 arguments:

| Argument | Description | Value(s) | Meanings | Omit | Remark |
| --------- | --- | ---- | ---- | --- | ---- |
| type  | Data type | 0/1/2  |<ul><li>0 : Gaussian</li><li>1: Binary</li><li>2: survival</li></ul>  | ✖  | -  |
| method | Method for handling missing data | 0/1  |<ul><li>0 : Complete</li><li>1: Impute & Joint</li></ul>  | ✖  | -  |
| penaltyno | Penalty type| 0  | <ul><li>0 : Complete</li></ul>  | ✖  | -  |
| sizeX  | Number of X  | All integer ≥ 0  || ✖  | - |
| r  | Numbers of latent variables |   | -  | ✖  | -  |
| groupsize  |Dimension of each latent variables  | |   | ✖  | -  |
| dirname  | Output directory | Any file path | -  | ✔  | <ul><li>Relative path can be used</li><li>Default : current working directory</li></ul>  |
| foldername  | Output folder name | Any name | -  | ✔  | Default `Result`  |

# Dataset

The input dataset should be in `.csv` format and consist of 3 components outcome variable `Y`, covariates `X` and potentially missing covariates `S`. Therefore, dataset is a `n x (p+k+1)` amatrix, where `n` is the sample size, `p` is the number of covariates and `k` is the number of potentially missing covariates. The dataset should be in following format:
|Outcome variable| 1st covariate |2nd covariate|...|pth covariate|1st missing covariate|2nd missing covariate|...|kth missing covariate|
|---|---|---|---|---|---|---|---|---|
||||||||||

*Sample dataset can be downloaded from [github page](https://github.com/alexwky/LASSO).

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

(Reference Paper)


