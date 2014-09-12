#DQS : Data Quality Services
[Context](https://github.com/Fleid/SQLSat-Paris-2014---DQS-MDS-PreConf/blob/master/README.md)

## The main driver : costs

**Direct costs**: easy to justify data quality efforts when impacts occur in the LoB

**Indirect costs**: you may not notice them at first, but they have consequences in the long term

VS

**Cost of optimizing data quality**: Prevention, Discovery, Cleaning (from easy to complex/costly)

#### Microsoft approach
- Cleansing : amend, remove or enrich data
- Matching : identify, link and merge related entries
- Profiling : analyze, identify issue (not really good in DQS)
- Monitoring : track and monitor (not really good in DQS)

What is cool : DQS is a Knowledge-Driven data quality solution. Let the business build a knowledge base, use that to check data quality.

What is uncool : the UI is bad. Bad bad.

## DQS : the tool
#### Artifacts
- Domain (===Attribute in MDS, column)
  - Domain values : list of correct / incorrect values (exact matching)
  - Reference data : external data references
  - Domain Rules : tests (regex, logical expressions, matching values)
  - Termbased relations : transcoding (inexact matching)

- Composite domain: (===Entity in MDS, table)
  - An address is Street + Zip Code + Country (domains)

#### First : Create the KB
By **Domain Discovery** from SQL Server or an Excel file (2003 XLS on 64bit servers). You can also import DQS files.

Then use **Domain Management** to edit and add things.

Little trick: if you import domain values from Excel on the format Column1, Column2, Column3... then DQS will create the Column1 value and associate Column2 and Column3 as synonyms.

#### Second : Create a DQ Project
The project will use the KB to actually clean data. It maps columns from the source data to domains and checks values.

