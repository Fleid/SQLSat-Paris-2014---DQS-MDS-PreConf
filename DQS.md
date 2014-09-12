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

NB : only one instance of DQS per server, on the default instance;

## DQS : the tool
#### Artifacts
- Domain (===Attribute in MDS, column)
  - Domain values : list of correct / incorrect values (exact matching)
  - Reference data : external data references (including web services)
  - Domain Rules : tests (regex, logical expressions, matching values)
  - Termbased relations : transcoding (inexact matching)

- Composite domain: (===Entity in MDS, table)
  - An address is Street + Zip Code + Country (domains)
  - You can do reference data checks on all the fields at once

#### First step : Create the KB (for cleansing)
By **Domain Discovery** from SQL Server or an Excel file (2003 XLS on 64bit servers). You can also import DQS files.

Then use **Domain Management** to edit and add things.

Little trick: if you import domain values from Excel on the format Column1, Column2, Column3... then DQS will create the Column1 value and associate Column2 and Column3 as synonyms.

#### Second step : Create a DQ Project (to actually clean data)
The project will use the KB to actually clean data. It maps columns from the source data (a copy of it in DQS) to domains and checks values. Then **you need to export the cleaned data** in SQL Server, Excel or CSV files.

Cool stuff : **domain parsing** with composing domain, splits a single column (domain) to multiple domains in the same composing domain

#### Third step : Matching
Detection of redundant data, after cleaning, even using fuzzy algos. Done in DQS using **matching policies** in the KB. Quite powerful but you have to determine your parameters manually :/

## DQS industrialization 
#### Automation
Using **SSIS**, you can access and use KBs in the data flow (no matching yet) with the "DQS Cleansing component". 

Using the **Excel MDS add-in**, you can access the matching policies. First enable the integration to DQS in the **MDS** management Web UI .

#### Best Practices
- Knowledge discovery in // using the trick described in [creating the KB](https://github.com/Fleid/SQLSat-Paris-2014---DQS-MDS-PreConf/blob/master/DQS.md#first-step--create-the-kb-for-cleansing)
- Exact matching >>> Similarity matching (performance wise), for every functions
  - Look for the 80/20 sweet spot: 80% of incoming values should hit the 20% of values that are always the same, and that should be defined as exact matching
- Define specific domains per language for text fields (UK, FR, DE...), use a conditional split to clean each subset on its own domain
- Use a conditional split, after the "DQS Cleansing component" and on its additional meta-data output columns (status, confidence, reason), to drive the ETL process
- Use the [Balanced Data Distributor](http://www.microsoft.com/en-us/download/details.aspx?id=4123) to parallelize the DQS cleansing when its recommended. Try [defining the default buffer size](https://connect.microsoft.com/SQLServer/feedback/details/713837/data-quality-services-dqs-cleansing-component-performance-too-slow) of the package to the capacity of the "DQS Cleansing component"
- 
