# rename _ct to _m

the output of the uni_mapping script creates a listing of all variables in the ACS Tables sql file definitions (K:\DataServices\Code\SQL\ACS\Tables).

for any missing or mis-matched variable names, items can be added to the "dictionary" section of uni_mapping script (in JSON format), or excluded using the "exclude_these_rows.csv" file.

after generating the output file: "column_ids2_censustracts_vhighpriority.csv" a duplicate file needs to be created for Municipalities, in which the table names are all updated to end with _m, instead of _ct.

this py notebook automates the renaming formerly run manually each time.

running this py notebook will overwrite the previous version of the file: column_ids2_muni_vhighpriority.csv.

edited 2021-12-15
