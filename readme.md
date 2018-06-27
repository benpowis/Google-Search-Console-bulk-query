## Google Search Console Bulk Query Exporter into Google BigQuery

This version of the Google Search Console Bulk Query requester builds upon the work of the following project:
https://github.com/stephan765/Google-Search-Console-bulk-query

### Introduction

Full credit for the code goes to the project liked above where this copy has been forked from.
Since Google Search Console now allows users to export up to 16 months of historic data I was iterested in exporting this to Google BigQuery for
 further analysis. I;ve added functionality to the original code which, in addition to creating a CSV of the results, also uploads them into a BigQuery table.
 
### Setup
For excellent instructions on setting up and using the original code, including activating the API and creating OAuth credentials, see this blog post:
https://moz.com/blog/how-to-get-search-console-data-api-python

In order to setup the BigQuery export open up the main .py file and replace the plceholder credentials with those of your account:

- project_id = "PROJECT_ID"
- pkey = 'MY_PRIVATE_KEY.json'
- my_table = 'MYDATESET.MYTABLE'
- import_action = 'append' # 'replace' will overwrite the table if it exists, 'fail' will not overwrite the table if it exists.

**The BigQuery table**: Column headers are *not* included in the data sent to BigQuery, so make the table before you begin, with the following Schema:

Inline-style: 
![alt text](https://image.ibb.co/mk9EEo/Capture.png "Sample BigQuery schema")

### Changes
Further details on the changes I have made to the original code:
- We now import pandas and gbq moduels.
- By default the code now creates a .csv outpul file AND pushes to BigQuery, if you want one of these processes removed simply comment out the appropriate row of the loop around line 285.
- I've added some additional columns to the data, so by default you will get `keyword`, `page`, `clicks`, `impressions`, `clickthrogh rate`, `average position`.
- Since all your data goes into the same table (by default), I have also added a `Date` column to the output.
