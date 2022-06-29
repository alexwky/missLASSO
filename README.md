**Table of Contents**

- [LASSO](#LASSO)
- [DOWNLOAD AND INSTALLATION](#download-and-installation)
- [Arguments](#Arguments)
- [Dataset](#Dataset)
- [Result](#Result)
- [Contact](#Contact)
- [Reference](#Reference)

# LASSO 
`LASSO` is a C++ software package that perform penalized-likelihood approach for multiple typee of many features with missing data using expectation-maximization (EM) algorithm. We use a latent variable model to characterize the relationships across and within data types and to infer missing values from observed data. We develop a penalized-likelihood approach for variable selection and parameter estimation and devise an efficient expectation-maximization (EM) algorithm to implement our approach. We establish the asymptotic properties of the proposed estimators when the number of features increases at a polynomial rate of the sample size. 

# DOWNLOAD AND INSTALLATION
## Download
The latest version of LASSO can be downloaded from [github page](https://github.com/alexwky/LASSO).

## Installation
`LASSO` is an executable file. Users can run it on both Linux and Window environment using `LASSO.tar.gz` or `LASSO.exe` respectively.
### Linux Environment
1. Download `LASSO.tar.gz` to the destination directory
2. Go to the directory that have `LASSO.tar.gz`
    ```
    cd ./[destination directory]
    ```
3. Extract `LASSO.tar.gz`
    ```
    tar -xzvf LASSO.tar.gz
    ```
4. Run `LASSO` 
    ```
    ./LASSO [type] [method] [penaltyno] [sizeX] [r] [groupsize] [cv] [lambda] [dirname] [foldername] [filename]
    Example : C:\Users\Desktop\LASSO>LASSO type 0 method 1 penaltyno 0 sizeX 0 r 1,1,1,1 groupsize 30,30,30 cv 1 lambda TestLambda.csv foldername testing filename SampleDataset.csv 
    ```
### Window Environment
1. Download `LASSO.exe` to the destionation directory
2. Open command prompt and set the working directory
    ```
    cd ./[destination directory]
    ```
3. Run `LASSO`
    ```
    LASSO [type] [method] [penaltyno] [sizeX] [r] [groupsize] [cv] [lambda] [dirname] [foldername] [filename]
    Example : C:\Users\Desktop\LASSO>LASSO type 0 method 1 penaltyno 0 sizeX 0 r 1,1,1,1 groupsize 30,30,30 cv 1 lambda TestLambda.csv foldername testing filename SampleDataset.csv 
    ```

# Arguments

There are 11 arguments that users have to input to the executable file through command prompt. Please read the following table for the details of the 8 arguments:

| Argument | Description | Value(s) / Format | Meanings | Omit | Remark |
| --------- | --- | ---- | ---- | --- | ---- |
| type  | Data type | 0/1/2  |<ul><li>0 : Gaussian</li><li>1: Binary</li><li>2: survival</li></ul>  | ✖  | -  |
| method | Method for handling missing data | 0/1  |<ul><li>0 : Complete</li><li>1: Impute & Joint</li></ul>  | ✖  | -  |
| penaltyno | Penalty type| 0  | <ul><li>0 : Complete</li></ul>  | ✖  | -  |
| sizeX  | Number of covariate | All integer ≥ 0  || ✖  | - |
| r  | Numbers of latent variables |   | -  | ✖  | seperate using ","  |
| groupsize  |Dimension of each latent variables  | | - | ✖  | seperate using ","  |
| cv  |Cross-Validation|0/1 |<ul><li>0 : Don't do Cross-Validation </li><li>1: Do Cross-Validation</li> | ✔  | -  |
| lambda  |lambda series | .csv file | - | ✔ | -  |
| dirname  | Output directory | Any file path | -  | ✔  | <ul><li>Relative path can be used</li><li>Default : current working directory</li></ul>  |
| foldername  | Output folder name | Any name | -  | ✔  | Default `Result`  |
| filename  | Input dataset name | .csv file | -  | ✖  | - |


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

Wong, K. Y., Zeng, D., and Lin, D. Y. (2021), "Penalized Regression for Multiple Types of Many Features With Missing Data," Statistica Sinica [online], DOI: 10.5705/ss.202020.0401.


