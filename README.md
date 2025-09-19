# marcmatchcheck
Python. Compares MARC records across key fields (ISBN, author, title, edition, publisher, publication date, and physical description) by matching on 001. Requires input of two .mrc files with matching 001s and returns .csv with key fields and similarity score using fuzz.WRatio.
Compares different versions of the same MARC records across key fields (ISBN, author, title, edition, publisher, publication date, and physical description) by matching on 001. Requires input of two .mrc files with matching 001s and returns .csv with key fields and similarity score using fuzz.WRatio.

NOTE: The original version of this program was created with the assistance of Microsoft Copilot and Meta AI. This version has been fully reviewed manually, but may still include some inefficiencies. Use with caution.

Inputs
•Two .mrc (MARC Binary) files with matching 001 fields (e.g., different versions of the same records)

Outputs
•Uniquely named output file with key fields from records and average similarity score
•Non-unique files from process for use troubleshooting

Function
•Accepts text arguments for file names (without extensions)
•Retrieves key fields from records using PyMarc including: ISBN (020, first occurrence only), author (100, 110, or 111), title (245 $a and $b), edition statement (250) publisher (260 $b or 264 $b), publication date (260 $c or 264 $c), physical description (300)
•Creates two dataframes, one for each input file
•Merges the dataframes using 001 as the key
•Calculates similarity between record A and recrd B
    •Returns 100 for exact ISBN match (including None) or 0 for mis-match
    •Uses fuzz.WRatio to calculate similarity of all other fields (including None)
    •Returns average of all similarity scores rounded to two decimal places
•Adds column with similarity scores to start of dataframe with merged records and sorts on similarity score •Writes results to a new CSV using timestamp (month, day, hour, minute) to avoid overwriting earlier outputs

Warnings/Areas for Improvement
•Doesn't account for records with multiple ISBNs 
•Doesn't flag records where "updated" version is missing key fields in "original" version (NOTE: in earlier testing this often happened because original versions of records were improperly coded)
