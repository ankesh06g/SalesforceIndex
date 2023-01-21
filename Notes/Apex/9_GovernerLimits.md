# Governer Limits

> **Note:**
> Although scheduled Apex is an asynchronous feature, synchronous limits apply to scheduled Apex jobs.

| Description                                | Synchronous | Asynchronous |
|--------------------------------------------|-------------|--------------|
| SOQL Queries | 100 | 200 |
| - records retrieved by SOQL queries | 50,000 | 50,000 |
| - records retrieved by Database.getQueryLocator | 10,000 | 10,000 |
| SOSL queries | 20 | 20 |
| - records retrieved by a single SOSL query | 2,000 | 2,000 |
| DML statements | 150 | 150 |
| number of records processed as a result of DML statements, Approval.process, or database.emptyRecycleBin | 10,000 | 10,000 |
| callouts | 100 | 100 |
| - cumulative timeout for all callouts | 120 sec | 120 sec |
| Future methods per Apex invocation | 50 | 1 |
| heap size | 6 MB | 12 MB |
| 
