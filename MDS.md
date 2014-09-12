#MDS : Master Data Services
[Context](https://github.com/Fleid/SQLSat-Paris-2014---DQS-MDS-PreConf/blob/master/README.md)

## MDS, MDM ?
The **problem** that MDS tries to solve is MDM (Master Data Management): define core identities in the company (a customer, a product...) and have the same entities used everywhere in all applications

MDM lives in **2 places** : between LoBs, (MDM operational), and between LoBs and DWH (MDM analytical)

How to build a MDM solution **the right way** : vision > strategy > tactics > organization > tools
Usual way to build a MDM solution : organization & tools > failure

## Microsoft approach 
> We are an open platform, do what you want with it.

Generic tools, Framework, no vertical/domain solution, no further costs
artifacts
<img src="https://github.com/Fleid/SQLSat-Paris-2014---DQS-MDS-PreConf/blob/master/img/MDS1.JPG" width="600">

## MDS Artifacts

- Models
  - Entities
    - Attributes
    - Members
  - Hierarchies
    - Derived (generated from a domain-based attribute relationship)
	- Explicit (everything required is in the same entity)
  - Collections
  - Versions

## Interfaces  

Web UI and Excel. **Web UI sucks**. Excel add-in is great. Only thing not available in Excel yet is Hierarchies management.

With the web interface you can't edit artifacts, you have to drop them and recreate them. In Excel you can... In Excel you can generate Domain based constraints (enforced lookups) on the fly, loaded from the actual field.

## Business Rules

Data owners write rules in pseudo-natural language, applied to attribute members for validation. But is has to be done in the **Web UI** :/

Domain based look-ups are not possible at the moment. **Rules can only work at the entity level (row level)**.

**Rules can trigger** email notifications (Web UI) and other work-flow options (via Service Broker).

## Work-flows

Only **simple approval work-flows** can be created (manually, with change tracking and email notifications). If more is needed, add external DLL via .NET, or do SharePoint integration (independently of MDS, just on XLSX files).

## Security

Integrated with Active Directory. Manage user permissions and assignments to specific functions, models and attributes **(column level)** and hierarchy levels or members **(row level)**. Everything is done in the Web UI.

## Import/Export
### Staging

Each entity has a stage (SQL tables : stg.***.Leaf). It's a generic architecture, managed in batches through views and stored procedures.

A flag is present in each staging table, that will drive the batch, for each row:

- 0 / blank : Optimistic Merge
- 1 : Insert
- 2 : Overwrite Merge
- 3 : Delete
- 4 : Purge
- 5 : Delete Overwrite
- 6 : Purge Overwrite

Use SSIS to load the staging tables, and launch the required SP.

### Deployment scenarios

3 options : full model, model updates (new objects), partial model deployment (selected objects). Note that the .PKG file generated for deployment does not contain : user defined meta-data, file attributes and user/group permissions (that's ok, it's security related data that should be different in each environment)

### Exporting data

You have to create a subscription view (Web UI) to expose data for each entity. Note that if the structure of the entity changes, you have to recreate the view.
