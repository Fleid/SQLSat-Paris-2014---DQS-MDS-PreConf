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
- Profiling : analyse, identify issue (not really good in DQS)
- Monitoring : track and monitor (not really good in DQS)

What is cool : DQS is a Knowledge-Driven data quality solution. Let the business build a knowledge base, use that to check data quality.

What is uncool : the UI is bad. Bad bad.

## DQS : the tool
#### Artifacts
- Domain concept (===Entity in MDS)
- Domain (===Attribute in MDS)
  - Domain values : list of correct / incorrect values
  - Reference data : external data
  - Rules : tests
  - Termbased relations : 

