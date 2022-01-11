__alter columns query__

in order to update the data type of a large number of columns at once, you can run an information schema query, then format the columns found into ALTER TYPE statements which can be run all at once.

this script uses jinja template to transform a plain-text csv list of column names into a set of ALTER statements.

here is a sample query for the information schema in postgres:

SELECT 'COLUMNS: ' || string_agg(c.column_name, ', ') As sqlstmt
FROM information_schema.columns As c
WHERE table_name = 'data_table_X' AND
      c.column_name NOT LIKE '%me'AND
      c.column_name NOT LIKE '%mep'AND
      c.column_name NOT LIKE '%p'AND
      c.column_name NOT IN ('seq_id', 'muni_id', 'municipal', 'geoid', 'logrecno', 'acs_year')
GROUP BY c.table_name;

This will find all the columns in 'data_table_X'  that do not end with the letters me, mep, or p, and it ignores the standard columns for MAPC metadata, like muni_id, geoid...

After this query is run, the output list of column names can be processed and run through this python notebook, which will auto-generate all the ALTER COLUMN statements in one go.

_input:_

alter_input folder is where the plain_text.csv file is placed, along with the template.json file that controls the output format.

_configuration:_

set the following parameters in "alter_compile_from_csv", for example

1. table_name = "b25117"
2. type = "B25117"
3. input = "b25117_dict"

__table_name__ is the prefix for the output file.
__type__ is the new data type to be applied to all columns
__input__ is the filename of the list of columns

_output:_

run the py notebook, see results in alter_output folder.

the output will be a text file in __table_name_alter.txt__ and will contain all sequel statements.  

Note:  before you run the complete set of statements remove the final comma before the closing semi-colon.

__video demo__  if you want to see the whole process of running the first information schema query, then cleaning the list and running the python notebook, as well as committing the final ALTER COLUMN statements, here is a video [(5 min)](https://www.youtube.com/watch?v=ReruI_ZelLA)

