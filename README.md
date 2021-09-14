# LASSO
LASSO is a program that perform penalized-likelihood approach for multiple typee of many features with missing data using expectation-maximization (EM) algorithm.

# Installation #

LASSO is an executable file. Run `LASSO.exe` through command prompt with a vector of arguments and an organized dataset.
Example
```
cd <LASSO_REPO_PATH>
LASSO type 0 method 0 penaltyno 0 sizeX 0 r 1,1,1,1 groupsize 20,30,40
```

# Arguments #

There are 8 arguments that users have to input to the executable file through command prompt. Please read the following table for the details of the 8 arguments:

| Argument | Description | Value(s) | Meanings | Omit | Remark |
| --------- | --- | ---- | ---- | --- | ---- |
| type  | Data type | 0/1/2  |<ul><li>0 : Gaussian</li><li>1: Binary</li><li>2: survival</li></ul>  | ✖  | -  |
| method | Method for handling missing data | 0/1  |<ul><li>0 : Complete</li><li>1: Impute & Joint</li></ul>  | ✖  | -  |
| penaltyno | Penalty type| 0  | <ul><li>0 : Complete</li></ul>  | ✖  | -  |
| sizeX  | Number of X  | All integer ≥ 0  || ✖  | - |
| r  | Numbers of latent variables |   | -  | ✖  | -  |
| groupsize  |  | |   | ✖  | -  |
| dirname  | Output directory | Any file path | -  | ✔  | <ul><li>Relative path can be used</li><li>Default : current working directory</li></ul>  |
| foldername  | Output folder name | Any name | -  | ✔  | Default `Result`  |

# Dataset #

The input dataset consist of 3 components outcome variable `Y`, covariates `X` and potentially missing covariates `S`. Therefore, dataset is a `n x (p+k+1)` amatrix, where `n` is the sample size, `p` is the number of covariates and `k` is the number of potentially missing covariates. The dataset should be in following format:
|Outcome variable| 1st covariate |2nd covariate|...|pth covariate|1st missing covariate|2nd missing covariate|...|kth missing covariate|
|---|---|---|---|---|---|---|---|---|
||||||||||

# Result #

The results will be stored in an output folder. By default, the output folder is called "Result" under current working directory. The output folder consist of following `.csv` files:

`Complete mode`
 1. Complete.csv
 2. Completye-lambda.csv
 3. Complete-loglikelihood.csv
 
`Impute & Joint mode`
 1. Impute.csv
 2. Impute-imploglikelihood.csv
 3. Impute-lambda.csv
 4. Impute-loglikelihood.csv
 5. Impute-param.csv
 6. Joint.csv
 7. Joint-lambda.csv
 8. Joint-loglikelihood.csv
 9. Joint-param.csv

# Contact #

Wong Kin Yau, Alex <<kin-yau.wong@polyu.edu.hk>>

# Reference #

(Reference Paper)


