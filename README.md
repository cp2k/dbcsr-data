# DBCSR-data

This repository contains the data resulting from the autotuning of [libcusmm](https://github.com/cp2k/dbcsr/tree/develop/src/acc/libsmm_acc/libcusmm) kernels.

This data can be used as training data for the [predictive modeling of optimal parameters for libcusmm](https://github.com/cp2k/dbcsr/tree/develop/src/acc/libsmm_acc/libcusmm/predict.md).

![libcusmm parameters](images/libcusmm_parameters_and_memory.png)

## File Contents Description

Raw kernel parameters and their measured performance are recorded in CSV files. Parameters for different algorithms are recorded in different files:

- `raw_training_data_largeDB1.csv`
- `raw_training_data_largeDB2.csv`
- `raw_training_data_medium.csv`
- `raw_training_data_small.csv`
- `raw_training_data_tiny.csv`

## Contributing

##### Download data from this repository

- After downloading data, concatenate CSV files that have been split in multiple files under 2GB using:

```%bash
$ cat raw_training_data_ALGORITHM_* >> raw_training_data_ALGORITHM.csv
```

##### Collect new libcusmm autotuning data

- Follow the instructions in the [predictive modeling of optimal parameters for libcusmm](https://github.com/cp2k/dbcsr/tree/develop/src/acc/libsmm_acc/libcusmm/predict.md).

##### Contribute your collected data back to this repository

- To store large CSV files, this repository uses [Git Large File Storage (git-lfs)](https://git-lfs.github.com/), which you will have to install. 

- Github does not support adding LFS objects [larger than 2GB](https://github.community/t5/Support-Protips/Working-with-large-files-and-repositories/ba-p/9343). Split your CSV files larger than 2GB using: 

```%bash
$ split -a 1 -b 2000m raw_training_data_ALGORITHM.csv raw_training_data_ALGORITHM_ 
$ for file in raw_training_data_ALGORITHM_*; do mv $file $file.csv; done
```

- As a commit message, follow the [git commit template](git-commit.template) in order to reliably associate relevant metadata to the data you collected.
