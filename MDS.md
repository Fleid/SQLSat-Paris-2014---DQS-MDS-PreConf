#MDS : Master Data Services
[Context](https://github.com/Fleid/SQLSat-Paris-2014---DQS-MDS-PreConf/blob/master/README.md)

## MDS, MDM ?
The **problem** that MDS tries to solve is MDM (Master Data Management): define core identities in the company (a customer, a product...) and have the same entities used everywhere in all applications

MDM lives in **2 places** : between LoBs, (MDM operational), and between LoBs and DWH (MDM analytical)

How to build a MDM solution **the right way** : vision > strategy > tactics > organisation > tools
Usual way to build a MDM solution : organisation & tools > failure

## Microsoft approach 
> We are an open platform, do what you want with it.

Generic tools, Framework, no vertical/domain solution, no further costs
artefacts
<img src="https://github.com/Fleid/SQLSat-Paris-2014---DQS-MDS-PreConf/blob/master/img/MDS1.JPG" width="600">

## MDS Artefacts

- Models
  - Entities
    - Attributes
    - Members
  - Hierarchies
    - Derived
	- Explicit
  - Collections
  - Versions

## Interfaces  

Web and Excel. **Web sucks**. Excel add-in is great. Only thing not available in Excel yet is Hierarchies management.

With the web interface you can't edit artefacts, you have to drop them and recreate them. In Excel you can... In Excel you can generate Domain based constraints (enforced lookups) on the fly, loaded from the actual field.
