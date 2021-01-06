# NLP-Search-Engine-COVID-19-Dataset
Python based implementation of NLP-Search-Engine to search result for given Natural Language Query from [Covid-19 Dataset](https://github.com/datasets/covid-19).

## Dependencies
Install the following python3 packages to your python environment:
- ```Spacy``` (with 'en_core_web_sm')
- ```SUTime``` ([Instructions](https://github.com/FraBle/python-sutime))
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

- In ```query-search.ipynb``` second code-block contains the necessary paths and flags. Change them accordingly:
    - **database_path** - File path where you stored your previously generated sqlite3 database
    - **parsed_parameter_save_path** - File path where you stored previously generated parameters for given queries.
    - **print_sql_queries** - Set True if you want to output the executed SQL query along with the result


## How to Run
- Open ```nlp-search-engine.ipynb``` and ```query-search.ipynb``` in jupyter notebook.
- Execute all cells of ```nlp-search-engine.ipynb``` to extarct parameters from queries provided in [possible-questions.txt](https://github.com/Anshul718/NLP-Search-Engine-COVID-19-Dataset/blob/main/possible-questions.txt)
- Then execute all the cells of ```query-search.ipynb``` to generate the final result.

## Examples
1. **Input Query** - Which country saw highest number of death in the month of April?<br>
   **Extracted Parameters** - <br>
        {<br>
       'query': 'Which country saw highest number of death in the month of April?',<br>
       'Place': {'no_match': [], 'states': [], 'countries': []},<br>
       'Time Duration': {'begin': '2020-04-01', 'end': '2020-04-31'},<br>
       'Case Type': 'death',<br>
       'Function Type': 'maximum',<br>
       'Operation Type': 'country'<br>
       }<br>
    **Generated SQL** - <br>```SELECT Country FROM (SELECT Country, (MAX(sum)-MIN(sum)) as cases FROM (SELECT Date, Country, SUM(Deaths) as sum FROM countries_aggregated WHERE Date BETWEEN '2020-04-01' AND '2020-04-31' GROUP BY Date, Country) GROUP BY Country) WHERE cases = (SELECT MAX(cases) from (SELECT Country, (MAX(sum)-MIN(sum)) as cases FROM (SELECT Date, Country, SUM(Deaths) as sum FROM countries_aggregated WHERE Date BETWEEN '2020-04-01' AND '2020-04-31' GROUP BY Date, Country) GROUP BY Country));```<br>
    **Final Answer** - US

2. **Input Query** - total number of new cases found in Greece between april to september?<br>
   **Extracted Parameters** - <br>
        {<br>
        'query': 'total number of new cases found in Greece between april to september?',<br>
        'Place': {'no_match': [], 'states': [], 'countries': ['greece']},<br>
        'Time Duration': {'begin': '2020-04-01', 'end': '2020-09-31'},<br>
        'Case Type': 'confirm',<br>
        'Function Type': 'sum',<br>
        'Operation Type': 'cases'<br>
       }<br>
    **Generated SQL** - <br>```SELECT Confirmed FROM countries_aggregated WHERE Country = 'Greece' AND Date BETWEEN '2020-04-01' AND '2020-09-31';```<br>
    **Final Answer** - 17060