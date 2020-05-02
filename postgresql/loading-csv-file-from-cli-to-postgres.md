# Loading CSV File from CLI to Postgres

Today I learned how to load a very large CSV file to the Postgres database using the command line.

Half a million rows loaded in mere seconds locally whereas they would have taken years. 

Caveats:

* The columns in the table have to match _exactly_ the fields in the CSV (unless you feel like munging ahead of time
* Test test test with small files, then move up
* Use the writer role if you can, but the DBA account if you have to
* You will probably run into issues with column types/widths.  Have PGAdmin running while you attempt

```
COPY ***table_name*** 
FROM '/complete/file/path/or/you/will/be/sorry.csv' DELIMITER ',' CSV HEADER;
```