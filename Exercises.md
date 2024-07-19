###Exercise - 1: 
1) Read and understand - ACID features. What each term means ?        
2) Run and explore each keyword in the notebook - Delta101.ipynb 
3)      Read about time travel feature. 
        Save to an external table (specify location)  
        Explore the Delta Transaction log
        Can you query the transaction log using spark sql - Find out more about it.
        Make more changes and go back in time.


###Exercise - 2 using bootloader.json - To train and test concepts on Schema Evolution, Time Travel, Merge
2.1 Create and save a parquet file with top 1000 records. A sample json source record is pasted here - {"category":"Sports","event_name":"View Project","gender":"M","age":"18-24","marital_status":"married","session_id":"69f62d2ae87640f5a2dde2b2e9229fe6","device":"android","client_time":1393632004,"location":{"latitude":40.189788,"city":"Lyons","state":"CO","longitude":-105.35528,"zip_code":"80540"}} 
    Add a new column row_number using the window functions. 
2.2 Using the parquet file from above step, create a delta table (ref: user_profile) with first 200 records and the following 6 fields - category, gender, age, marital_status, session_id, client_time 
2.3 Append another 200 records from the parquet into the delta table user_profile.
2.4 Inspect the table history . Use time travel feature , to query the records as of step 2.2. The record count should only be 200 in this version.
2.5 Add two new columns into the table a) visit_timestamp in YYYY-MM-DD HH:MM:SS format using the existing column client_time which is in unix format. b)updated_at (timestamp) value as current_timestamp 
2.6 Query the records to see the outcome of step 2.5
2.7 Read first 200 records from the parquet file and MERGE into the user_profile table, by matching on the session_id. 
    When there is a match, update the fields from source side and for the  updated_at use current_timestamp
    When there is no match, Insert 
2.8 RESTORE the delta table to that of version as of step 2.5 (i.e before MERGE operation)
