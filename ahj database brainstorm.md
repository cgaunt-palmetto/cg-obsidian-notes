

### Step 1
Create a interim staging model for AHJs in the datawarehouse
Get PR approved and merged

### Step 2
Create an AHJ view file in Looker on a new branch against Business-Intelligence

### Step 3
Turn `tmp_salesforce_job_history` into a `salesforce_job_history_trunk`
Add first permit submission date to `salesforce_job_history_trunk`
Rewire tmp_job_history in Looker (BI layer) to connect to job_history_trunk

### Step 4
Discuss with Mariah and team on where to best put the permitting_job_position_against_ahj_verification in the data warehouse. Currently thinking that an intermediate table is the right move, as hosting in Looker will impact performance in the long run.

### Step 5
Bring in contact requirements mapping table to Looker BI layer

### Step 6
Join them all in the solar projects explore
    alchemy contact table
    alchemy opportunity table
    ahjs table
    contact requirements mapping table

### Step 7
Deliver to Bonnie et. al