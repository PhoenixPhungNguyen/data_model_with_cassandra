# Project: Data Modeling with Cassandra

## Project Overview
This project demonstrates **ETL and data modeling using Apache Cassandra**.  
The goal was to design **query-driven tables** optimized for retrieving music app user history.

### 1. music_app_history
- **Partition Key:** `session_id`  
- **Clustering Column:** `item_in_session`  
- **Purpose:** Efficiently retrieve artist, song, and length for a specific session and item.

```sql
CREATE TABLE IF NOT EXISTS music_app_history (
    session_id int,
    item_in_session int,
    artist text,
    song text,
    length float,
    PRIMARY KEY (session_id, item_in_session)
);
```
---

## **3️⃣ Table 2 – user_session_songs**

### 2. user_session_songs
- **Partition Key:** `(user_id, session_id)`  
- **Clustering Column:** `item_in_session`  
- **Purpose:** Retrieve all songs for a user in a session in order.

```sql
CREATE TABLE IF NOT EXISTS user_session_songs (
    user_id int,
    session_id int,
    item_in_session int,
    artist text,
    song text,
    first_name text,
    last_name text,
    PRIMARY KEY ((user_id, session_id), item_in_session)
);
```

## **4️⃣ Table 3 – song_listeners**

### 3. song_listeners
- **Partition Key:** `song`  
- **Clustering Columns:** `user_id, first_name, last_name`  
- **Purpose:** Lookup all users who listened to a specific song.

```sql
CREATE TABLE IF NOT EXISTS song_listeners (
    song text,
    user_id int,
    first_name text,
    last_name text,
    PRIMARY KEY (song, user_id, first_name, last_name)
);
```
---

## **5️⃣ ETL & Query Details**
- Data loaded from `event_datafile_new.csv`.  
- INSERT statements aligned with Cassandra’s **query-driven design**.  
- SELECT statements used to **validate data entries**.  
- Schema naming conventions use **snake_case** for clarity.
  
## Reviewer Feedback
> "Congratulations! Your dedication has resulted in an **outstanding Data Model with Cassandra**.  
> All rubric criteria are met, including schema design, primary key definitions, and query-driven optimization. Excellent work!"

## Notes / Lessons Learned
- Proper **partition and clustering key design** is critical for query performance in Cassandra.  
- Naming conventions and query-driven tables make ETL and validation straightforward.  
- Understanding **how queries dictate table design** is essential in NoSQL modeling.
