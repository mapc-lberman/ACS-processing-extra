__dictionary compiler__

to assist the manual editing of the dictionary entries added to the "uni-mapping" python script, this script uses jinja template to transform a plain-text csv list of variable names into the JSON dictionary format.

_input:_

dict_input folder is where the plain_text.csv file is placed, along with the template.json file that controls the output format.

_configuration:_

set the following parameters in "dict_compile_from_csv", for example

1.  table_name = "b25117_hu_tenure_by_fuel_acs_m"
2. group = "B25117"
3. new_dict = "b25117_dict"

_output:_

run the py notebook, see results in dict_output folder.

the *Results.csv file should have all the variables transformed into the default JSON entries.  Note:  these will need to be edited for their correct Universe and Margin of Error values, and the moe, percent boolean changed as needed.