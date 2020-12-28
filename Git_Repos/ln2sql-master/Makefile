clean:
	rm -rf *.json *.pyc
test:
	pytest
	rm -rf *.json *.pyc
lint:
	pep8 .
run:
	python -m ln2sql.main -d "D:\My Study Folder\Others\NLP-Search-Engine-COVID-19-Dataset\dataset\covid-19\mysql_database\final-schema-small.sql" -l lang_store/english.csv -j output.json -t thesaurus_store/th_english.dat -i "number of Confirmed Cases in US between August and December?"

