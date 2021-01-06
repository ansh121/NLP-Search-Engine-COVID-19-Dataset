# NLP-Search-Engine-COVID-19-Dataset
Python based implementation of NLP-Search-Engine to search result for given Natural Language Query from [Covid-19 Dataset](https://github.com/datasets/covid-19).

## Dependencies
Install the following python3 packages to your python environment:
- ```Spacy``` (with 'en_core_web_sm')
- ```SUTime ``` ([Instructions](https://github.com/FraBle/python-sutime))
- ```CSV```
- ```SQLite3```
- ```Pickle```
- ```re```

## Dataset
Download the [Covid-19 Dataset](https://github.com/datasets/covid-19), which contains CSV files for covid-19 statistics of various countries. Only 5 csv files are required to run this code:
    - worldwide-aggregate.csv
    - us_simplified.csv
    - reference.csv
    - time-series-19-covid-combined.csv
    - countries-aggregated.csv

## Change Required Paths
- In ```nlp-search-engine.ipynb``` second code-block contains the necessary paths and flags. Change them accordingly:
    - **query_file_path** - Path to your input query file
    - **create_database_flag** - Set True if you want to create database from CSV files (Required Initially)
    - **dataset_path** - Path to your covid-19 dataset CSV files folder
    - **database_path** - File path where you want to store your generated sqlite3 database
    - **parsed_parameter_save_path** - File path where you want to store generated parameters for given queries.

- In ```query-search.ipynb`` second code-block contains the necessary paths and flags. Change them accordingly:
    - **database_path** - File path where you stored your previously generated sqlite3 database
    - **parsed_parameter_save_path** - File path where you stored previously generated parameters for given queries.
    - **print_sql_queries** - Set True if you want to output the executed SQL query along with the result


## How to Run
- Open ```nlp-search-engine.ipynb``` and ```query-search.ipynb``` in jupyter notebook.
- Execute all cells of ```nlp-search-engine.ipynb``` to extarct parameters from queries provided in [possible-questions.txt](https://github.com/Anshul718/NLP-Search-Engine-COVID-19-Dataset/blob/main/possible-questions.txt)
- Then execute all the cells of ```query-search.ipynb``` to generate the final result.
