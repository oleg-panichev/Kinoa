# Kinoa
[![GitHub release](https://img.shields.io/badge/Version-0.0.2-blue.svg?style=for-the-badge)](https://github.com/oleg-panichev/kinoa)

Kinoa - a simple library to store your code and produced files after each run. It allows monitor, easily compare  and reproduce experiments with your code.

Tested on Python 3.5.* and 3.6.* only. 

## Installation
```sh
git clone https://github.com/oleg-panichev/kinoa.git
cd kinoa
python setup.py install
```

## Usage example
```python
from kinoa import kinoa

# Your code here

# Preparing for Kinoa
files = ['my_script.py', 'some_data.npy', 'results.csv']
experiment_name = 'My cool experiment'
params = {
    'n_of_iterations': 100,
}
scores = {
    'cv_accuracy': 1,
    'kaggle': 0.999,
}
other = {
    'k': 10,
}
comments = 'This is example.'
working_dir = ''
kinoa_dir_name = '__kinoa__'
columns_order = {
    'other.k': -3,
    'scores.cv_accuracy': -2,
    'scores.kaggle': -1,
}

# Saving results
kinoa.save(
    files,
    experiment_name=experiment_name,
    params=params,
    scores=scores,
    other=other,
    comments=comments,
    working_dir=working_dir,
    kinoa_dir_name=kinoa_dir_name, 
    use_spaces=False,
    sort_log_by='experiment_datetime', 
    sort_log_ascending=True,
    columns_order=columns_order,
)
```

Parameters:
```python
def save(files, experiment_name='', params={}, scores={}, other={}, 
         comments='', update_html_flag=False, working_dir='', 
         kinoa_dir_name='__kinoa__', use_spaces=False, 
         sort_log_by='experiment_datetime', sort_log_ascending=True, 
         columns_order=[])
```

- **files** *(list of str)* - List of files and directories to save.
- **experiment_name** *(str)* - String with name of an experiment. If empty - date and time used to define the name in a format *%Y-%m-%d_%H-%M-%S*.
- **params** *(dict)* - Dictionary with parameters of experiment.
- **scores** *(dict)* - Dictionary with evaluation results.
- **other** *(dict)* - Dictionary with other data needed in log.
- **comments** *(str)* - String with comments to the experiment.
- **working_dir** *(str)* - Path to the directory, where log of experiments will be stored. *kinoa_dir_name* directory will be created within working_dir.
- **kinoa_dir_name** *(str)* - Name of the directory, where logs will be stored.
- **use_spaces** *(bool)* - Flag if spaces should be used in a directory name for current experiment.
- **sort_log_by** *(str or list of str)* - Specify which columns to use to sort rows in the log file.
- **sort_log_ascending** *(bool or list of bool)* - Sort ascending vs. descending. Specify list for multiple sort orders. If this is a list of bools, must match the length of the sort_log_by.
- **columns_order** *(list of str or dict in format ('col_name': index))* - Specify order of columns in the log file. Columns that are not present in *columns_order* will remain in the file, but after specified columns.

After saving you may find all your experiments along with log file in *working_dir/kinoa_dir_name* directory. It will look like:
```
.
├── 2018-01-04_15-21-27_Decision_Tree_Classifier
│   ├── example.py
│   ├── example_directory_0
│   │   ├── example_file_in_directory_0.txt
│   │   └── example_file_in_directory_1.txt
│   └── example_directory_1
│       └── example_file_in_directory_1.txt
├── 2018-01-04_15-21-27_Logistic_Regression
│   ├── example.py
│   ├── example_directory_0
│   │   ├── example_file_in_directory_0.txt
│   │   └── example_file_in_directory_1.txt
│   └── example_directory_1
│       └── example_file_in_directory_0.txt
└── log.csv
```

See [examples/example.py](https://github.com/oleg-panichev/Kinoa/blob/master/examples/example.py) for more details.

## License
Apache License Version 2.0, January 2004

## Authors
- Oleg Panichev ([olegxpanichev@gmail.com](mailto:olegxpanichev@gmail.com))
