# Main Question
- What changes need to be made to the `salesforce_staging_generator` to make it scalable for other staging models outside of salesforce.

## Creation of Directories and File Names
Currently, the `salesforce_staging_generator` automatically creates a folder nested under the path `arbor/models/staging/salesforce_generated`. This folder is named by appending the table you are running the script on to the string `'salesforce_'`.

- To make this more scalable, we would need to do the following:
	- Change the base path on line 13 to be set to `arbor/models/staging`
	- Configure a user input to detail the source that is being leveraged by the script
		- append `_generated` to the source name and create the directory
		- the path.mkdir command should have the arg `exists=ok`
	- Keep the same logic for creating a directory reference on line 14
		- this will be `generated_{table_name called with script}`
	- Update the output path referenced on line 15 to match up with the above changes and spit out a relevant file name

## Updating the `get_data_from_snowflake` function
At the moment, two of the functions being called inside of the `get_data_from_snowflake` function on line 20 are hardcoded to reference Salesforce data: `get_salesforce_mappings` and `get_snapshot columns`

In order to make these more scalable, we will need to make some changes - either to the functions inside of `get_data_from_snowflake` or to the larger function itself.

#### Thoughts On Changes to `get_data_from_snowflake`
In order to be able to handle multiple data sources, it is possible that we will need to make functions similar to `get_salesforce_mappings` for the other data sources. 

I do not believe that we will be able to modularize the `get_salesforce_mappings` function as it does things that are specifically catered to the `salesforce_ripper` excerise we performed in order to pull out Salesforce label names that are shown in the UI.

Instead, I think that we will want to create specific functions for each data source that we are going to use this script for - and have the data source passed in as an argument to the python script

Today, we write `python3 scripts/salesforce_staging_generator account` to run the script on the Salesforce Account table, but I am imagining that we do something like the following:
	- `python3 scripts/staging_generator salesforce account`
	- `python3 scripts/staging_generator alchemy workflow_instances`
	- and so on

The downside of this approach being that we will have to write manual functions for each data source, rather than having a 'one-size fits all' model