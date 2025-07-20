# Python & SQL Quick Reference Cheat Sheets

## 🐍 **PYTHON ESSENTIALS**

### **Data Types & Variables**
```python
# BASIC TYPES
name = "Aman"                    # str
age = 28                         # int
salary = 75000.50                # float
is_remote = True                 # bool
skills = ["Python", "SQL"]       # list
config = {"host": "localhost"}   # dict

# TYPE CONVERSION
str(123)                         # "123"
int("456")                       # 456
float("78.9")                    # 78.9
list("hello")                    # ['h', 'e', 'l', 'l', 'o']

# STRING OPERATIONS
text = "Data Engineer"
text.upper()                     # "DATA ENGINEER"
text.lower()                     # "data engineer"
text.split()                     # ["Data", "Engineer"]
f"Hello {name}"                  # f-string formatting
```

### **Control Flow**
```python
# IF/ELSE
if age >= 18:
    status = "adult"
elif age >= 13:
    status = "teenager"
else:
    status = "child"

# FOR LOOPS
for skill in skills:
    print(f"I know {skill}")

# LIST COMPREHENSIONS (ESSENTIAL FOR DATA ENGINEERING)
numbers = [1, 2, 3, 4, 5]
squares = [x**2 for x in numbers]        # [1, 4, 9, 16, 25]
evens = [x for x in numbers if x % 2 == 0]  # [2, 4]

# WHILE LOOPS
count = 0
while count < 5:
    print(count)
    count += 1
```

### **Data Structures**
```python
# LISTS (MOST USED IN DATA ENGINEERING)
data = [1, 2, 3, 4, 5]
data.append(6)                   # [1, 2, 3, 4, 5, 6]
data.extend([7, 8])              # [1, 2, 3, 4, 5, 6, 7, 8]
data.pop()                       # removes last element
data.remove(3)                   # removes first occurrence of 3
data.sort()                      # sorts in place
sorted_data = sorted(data)       # returns new sorted list

# DICTIONARIES (CONFIGURATION & MAPPING)
config = {
    "database": "postgresql",
    "host": "localhost",
    "port": 5432
}
config["database"]               # "postgresql"
config.get("password", "default") # safe access with default
config.keys()                    # dict_keys(['database', 'host', 'port'])
config.values()                  # dict_values(['postgresql', 'localhost', 5432])

# SETS (UNIQUE VALUES)
unique_skills = {"Python", "SQL", "Python"}  # {"Python", "SQL"}
unique_skills.add("Databricks")
unique_skills.remove("SQL")
```

### **Functions & Error Handling**
```python
# FUNCTION DEFINITION
def calculate_salary(base, bonus=0):
    """Calculate total salary with optional bonus"""
    return base + bonus

# LAMBDA FUNCTIONS (USEFUL FOR DATA PROCESSING)
add = lambda x, y: x + y
multiply = lambda x, y: x * y

# ERROR HANDLING
try:
    result = 10 / 0
except ZeroDivisionError:
    result = "Cannot divide by zero"
except Exception as e:
    result = f"Error: {e}"
finally:
    print("Operation completed")

# DATA ENGINEERING PATTERN: SAFE DATA LOADING
def load_data_safely(file_path):
    try:
        with open(file_path, 'r') as file:
            return file.read()
    except FileNotFoundError:
        print(f"File {file_path} not found")
        return None
    except Exception as e:
        print(f"Error loading file: {e}")
        return None
```

### **File Operations**
```python
import json
import csv
import os

# FILE OPERATIONS
with open("data.txt", "r") as file:
    content = file.read()

with open("output.txt", "w") as file:
    file.write("Hello World")

# JSON PROCESSING (API RESPONSES, CONFIGS)
data = {"name": "Aman", "skills": ["Python", "SQL"]}
json_string = json.dumps(data)           # dict to JSON string
parsed_data = json.loads(json_string)    # JSON string to dict

# CSV PROCESSING (DATA ENGINEERING ESSENTIAL)
def read_csv_data(filename):
    data = []
    with open(filename, 'r') as file:
        reader = csv.DictReader(file)
        for row in reader:
            data.append(row)
    return data

def write_csv_data(filename, data):
    if not data:
        return
    with open(filename, 'w', newline='') as file:
        writer = csv.DictWriter(file, fieldnames=data[0].keys())
        writer.writeheader()
        writer.writerows(data)
```

### **Data Engineering Patterns**
```python
# CONFIGURATION MANAGEMENT
def get_database_config(environment="dev"):
    configs = {
        "dev": {"host": "localhost", "port": 5432},
        "prod": {"host": "prod-db.com", "port": 5432}
    }
    return configs.get(environment, configs["dev"])

# DATA VALIDATION PATTERN
def validate_data(data):
    errors = []
    for row in data:
        if not row.get('id'):
            errors.append(f"Missing ID in row: {row}")
        if not isinstance(row.get('value'), (int, float)):
            errors.append(f"Invalid value type in row: {row}")
    return errors

# DATA TRANSFORMATION PATTERN
def transform_data(data):
    transformed = []
    for row in data:
        transformed_row = {
            'id': row['id'],
            'value': float(row['value']),
            'timestamp': datetime.now().isoformat()
        }
        transformed.append(transformed_row)
    return transformed

# ERROR HANDLING PATTERN
def safe_data_operation(operation_func, *args, **kwargs):
    max_retries = 3
    for attempt in range(max_retries):
        try:
            return operation_func(*args, **kwargs)
        except Exception as e:
            if attempt == max_retries - 1:
                raise e
            print(f"Attempt {attempt + 1} failed: {e}")
            time.sleep(2 ** attempt)  # exponential backoff
```

---

## 🗄️ **SQL ESSENTIALS**

### **Basic Queries**
```sql
-- BASIC SELECT
SELECT column1, column2 FROM table_name;
SELECT * FROM users WHERE age > 25;

-- ALIASES
SELECT 
    user_id AS id,
    user_name AS name,
    created_at AS joined_date
FROM users;

-- DISTINCT VALUES
SELECT DISTINCT department FROM employees;

-- LIMITING RESULTS
SELECT * FROM orders ORDER BY order_date DESC LIMIT 10;

-- DATA ENGINEERING PATTERN: DATA PROFILING
SELECT 
    COUNT(*) as total_rows,
    COUNT(DISTINCT user_id) as unique_users,
    MIN(created_at) as earliest_date,
    MAX(created_at) as latest_date
FROM user_events;
```

### **WHERE Conditions & Aggregations**
```sql
-- WHERE CONDITIONS
SELECT * FROM users 
WHERE age BETWEEN 25 AND 35 
AND status = 'active'
AND email LIKE '%@gmail.com';

-- AGGREGATIONS
SELECT 
    department,
    COUNT(*) as employee_count,
    AVG(salary) as avg_salary,
    SUM(salary) as total_salary,
    MIN(salary) as min_salary,
    MAX(salary) as max_salary
FROM employees
GROUP BY department;

-- HAVING (FILTER AGGREGATED RESULTS)
SELECT 
    department,
    AVG(salary) as avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;

-- DATA ENGINEERING PATTERN: DATA QUALITY CHECK
SELECT 
    COUNT(*) as total_records,
    COUNT(CASE WHEN email IS NOT NULL THEN 1 END) as emails_filled,
    COUNT(CASE WHEN email LIKE '%@%' THEN 1 END) as valid_emails,
    ROUND(
        COUNT(CASE WHEN email LIKE '%@%' THEN 1 END) * 100.0 / COUNT(*), 
        2
    ) as email_completeness_percent
FROM users;
```

### **JOINs**
```sql
-- INNER JOIN (MOST COMMON)
SELECT 
    u.user_id,
    u.name,
    o.order_id,
    o.amount
FROM users u
INNER JOIN orders o ON u.user_id = o.user_id;

-- LEFT JOIN (KEEP ALL FROM LEFT TABLE)
SELECT 
    u.user_id,
    u.name,
    COUNT(o.order_id) as order_count
FROM users u
LEFT JOIN orders o ON u.user_id = o.user_id
GROUP BY u.user_id, u.name;

-- RIGHT JOIN (KEEP ALL FROM RIGHT TABLE)
SELECT 
    p.product_id,
    p.name,
    o.order_id
FROM products p
RIGHT JOIN order_items o ON p.product_id = o.product_id;

-- FULL OUTER JOIN (KEEP ALL FROM BOTH)
SELECT 
    u.user_id,
    o.order_id
FROM users u
FULL OUTER JOIN orders o ON u.user_id = o.user_id
WHERE u.user_id IS NULL OR o.order_id IS NULL;
```

### **Subqueries & CTEs**
```sql
-- SUBQUERY IN WHERE
SELECT * FROM employees 
WHERE salary > (SELECT AVG(salary) FROM employees);

-- SUBQUERY IN SELECT
SELECT 
    department,
    COUNT(*) as employee_count,
    (SELECT AVG(salary) FROM employees) as company_avg_salary
FROM employees
GROUP BY department;

-- COMMON TABLE EXPRESSIONS (CTEs)
WITH user_stats AS (
    SELECT 
        user_id,
        COUNT(*) as event_count,
        MAX(event_date) as last_event
    FROM user_events
    GROUP BY user_id
),
active_users AS (
    SELECT user_id
    FROM user_stats
    WHERE event_count > 10 
    AND last_event > CURRENT_DATE - INTERVAL '30 days'
)
SELECT 
    u.name,
    us.event_count
FROM users u
JOIN user_stats us ON u.user_id = us.user_id
JOIN active_users au ON u.user_id = au.user_id;
```

### **Window Functions**
```sql
-- ROW_NUMBER()
SELECT 
    name,
    salary,
    ROW_NUMBER() OVER (ORDER BY salary DESC) as salary_rank
FROM employees;

-- PARTITION BY
SELECT 
    department,
    name,
    salary,
    ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) as dept_rank
FROM employees;

-- LAG/LEAD (COMPARE WITH PREVIOUS/NEXT ROW)
SELECT 
    date,
    sales,
    LAG(sales) OVER (ORDER BY date) as prev_day_sales,
    LEAD(sales) OVER (ORDER BY date) as next_day_sales
FROM daily_sales;

-- RUNNING TOTALS
SELECT 
    date,
    sales,
    SUM(sales) OVER (ORDER BY date) as running_total
FROM daily_sales;

-- DATA ENGINEERING PATTERN: TIME-SERIES ANALYSIS
SELECT 
    user_id,
    event_date,
    event_type,
    COUNT(*) OVER (
        PARTITION BY user_id 
        ORDER BY event_date 
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) as events_last_7_days
FROM user_events;
```

### **Performance Optimization**
```sql
-- INDEXES (IMPROVE QUERY SPEED)
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_orders_user_date ON orders(user_id, order_date);

-- OPTIMIZED QUERIES
-- Instead of:
SELECT * FROM orders WHERE DATE(order_date) = '2024-01-01';

-- Use:
SELECT * FROM orders 
WHERE order_date >= '2024-01-01' 
AND order_date < '2024-01-02';

-- LIMIT WITH OFFSET FOR PAGINATION
SELECT * FROM users 
ORDER BY created_at 
LIMIT 100 OFFSET 200;  -- Page 3 (rows 201-300)

-- DATA ENGINEERING PATTERN: BATCH PROCESSING
SELECT 
    user_id,
    COUNT(*) as event_count
FROM user_events
WHERE event_date >= CURRENT_DATE - INTERVAL '1 day'
GROUP BY user_id
HAVING COUNT(*) > 100;  -- Only process active users
```

### **Data Engineering SQL Patterns**
```sql
-- DATA QUALITY CHECKS
SELECT 
    'duplicate_emails' as check_type,
    COUNT(*) as issue_count
FROM (
    SELECT email, COUNT(*)
    FROM users
    WHERE email IS NOT NULL
    GROUP BY email
    HAVING COUNT(*) > 1
) duplicates

UNION ALL

SELECT 
    'null_required_fields' as check_type,
    COUNT(*) as issue_count
FROM users
WHERE name IS NULL OR email IS NULL;

-- INCREMENTAL LOADING PATTERN
SELECT * FROM source_table
WHERE updated_at > (
    SELECT COALESCE(MAX(updated_at), '1900-01-01') 
    FROM target_table
);

-- DATA PARTITIONING
SELECT 
    DATE_TRUNC('month', order_date) as month,
    COUNT(*) as orders,
    SUM(amount) as revenue
FROM orders
WHERE order_date >= CURRENT_DATE - INTERVAL '12 months'
GROUP BY DATE_TRUNC('month', order_date)
ORDER BY month;

-- SCD TYPE 2 (SLOWLY CHANGING DIMENSIONS)
WITH current_records AS (
    SELECT 
        customer_id,
        name,
        email,
        valid_from,
        valid_to
    FROM customer_dimension
    WHERE valid_to IS NULL
),
new_records AS (
    SELECT 
        customer_id,
        name,
        email
    FROM customer_staging
)
SELECT 
    'update' as action,
    cr.customer_id
FROM current_records cr
JOIN new_records nr ON cr.customer_id = nr.customer_id
WHERE cr.name != nr.name OR cr.email != nr.email;
```

---

## 🔗 **PYTHON + SQL INTEGRATION**

### **Database Connectivity**
```python
# SQLALCHEMY SETUP
from sqlalchemy import create_engine, text
from sqlalchemy.orm import sessionmaker

# CONNECTION
engine = create_engine('postgresql://user:pass@localhost/dbname')
Session = sessionmaker(bind=engine)

# RAW SQL EXECUTION
def execute_query(sql, params=None):
    with engine.connect() as conn:
        result = conn.execute(text(sql), params or {})
        return result.fetchall()

# DATA ENGINEERING PATTERN: BATCH DATA LOADING
def load_data_batch(data, table_name, batch_size=1000):
    with engine.connect() as conn:
        for i in range(0, len(data), batch_size):
            batch = data[i:i + batch_size]
            # Convert batch to SQL insert
            conn.execute(text(f"INSERT INTO {table_name} VALUES ..."))
        conn.commit()

# CONFIGURATION PATTERN
class DatabaseConfig:
    def __init__(self, connection_string):
        self.engine = create_engine(connection_string)
        self.session = Session()
    
    def __enter__(self):
        return self
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        self.session.close()
```

### **Production-Ready Patterns**
```python
# COMPREHENSIVE ERROR HANDLING
import logging
import time
from typing import Optional, Dict, Any

class DataPipeline:
    def __init__(self, name: str):
        self.name = name
        self.logger = self._setup_logging()
    
    def _setup_logging(self):
        logging.basicConfig(
            level=logging.INFO,
            format='%(asctime)s - %(name)s - %(levelname)s - %(message)s'
        )
        return logging.getLogger(self.name)
    
    def run_with_retry(self, max_retries: int = 3):
        for attempt in range(max_retries):
            try:
                self.logger.info(f"Starting pipeline run {attempt + 1}")
                result = self._execute_pipeline()
                self.logger.info("Pipeline completed successfully")
                return result
            except Exception as e:
                self.logger.error(f"Attempt {attempt + 1} failed: {e}")
                if attempt == max_retries - 1:
                    raise
                time.sleep(2 ** attempt)  # exponential backoff
    
    def _execute_pipeline(self):
        # Your pipeline logic here
        pass

# DATA VALIDATION PATTERN
def validate_dataframe(df, rules: Dict[str, Any]) -> Dict[str, Any]:
    validation_results = {
        'passed': True,
        'errors': [],
        'warnings': []
    }
    
    for column, rule in rules.items():
        if column not in df.columns:
            validation_results['errors'].append(f"Missing column: {column}")
            validation_results['passed'] = False
            continue
        
        if 'not_null' in rule and df[column].isnull().any():
            validation_results['errors'].append(f"Null values found in {column}")
            validation_results['passed'] = False
        
        if 'unique' in rule and not df[column].is_unique:
            validation_results['warnings'].append(f"Duplicate values in {column}")
    
    return validation_results
```

---

## 📋 **ESSENTIAL IMPORTS FOR DATA ENGINEERING**

```python
# CORE IMPORTS
import pandas as pd
import numpy as np
from datetime import datetime, timedelta
import logging
from typing import List, Dict, Optional, Any
import json
import csv
import os
import time

# DATABASE IMPORTS
from sqlalchemy import create_engine, text
from sqlalchemy.orm import sessionmaker
import psycopg2

# DATA PROCESSING IMPORTS
import requests
from pathlib import Path
import yaml
import configparser
```

---

## 🎯 **QUICK REFERENCE COMMANDS**

### **Python Data Engineering Quick Reference**
```python
# DATA LOADING PATTERNS
def load_csv_safely(file_path: str) -> Optional[pd.DataFrame]:
    try:
        return pd.read_csv(file_path)
    except FileNotFoundError:
        logging.error(f"File not found: {file_path}")
        return None
    except Exception as e:
        logging.error(f"Error loading file: {e}")
        return None

# DATA VALIDATION
def validate_dataframe(df: pd.DataFrame, required_columns: List[str]) -> bool:
    missing_cols = set(required_columns) - set(df.columns)
    if missing_cols:
        logging.error(f"Missing columns: {missing_cols}")
        return False
    return True

# CONFIGURATION MANAGEMENT
def load_config(config_path: str) -> Dict[str, Any]:
    try:
        with open(config_path, 'r') as f:
            return json.load(f)
    except Exception as e:
        logging.error(f"Error loading config: {e}")
        return {}

# ERROR HANDLING PATTERN
def safe_operation(operation_func, *args, **kwargs):
    try:
        return operation_func(*args, **kwargs)
    except Exception as e:
        logging.error(f"Operation failed: {e}")
        raise
```

### **SQL Data Engineering Quick Reference**
```sql
-- DATA PROFILING
SELECT 
    COUNT(*) as total_rows,
    COUNT(DISTINCT column_name) as unique_values,
    COUNT(CASE WHEN column_name IS NULL THEN 1 END) as null_count,
    MIN(column_name) as min_value,
    MAX(column_name) as max_value,
    AVG(column_name) as avg_value
FROM table_name;

-- DATA QUALITY CHECK
SELECT 
    'duplicates' as issue_type,
    COUNT(*) as count
FROM (
    SELECT column_name, COUNT(*)
    FROM table_name
    GROUP BY column_name
    HAVING COUNT(*) > 1
) duplicates

UNION ALL

SELECT 
    'nulls' as issue_type,
    COUNT(*) as count
FROM table_name
WHERE column_name IS NULL;

-- INCREMENTAL LOADING
SELECT * FROM source_table
WHERE updated_at > (
    SELECT COALESCE(MAX(updated_at), '1900-01-01') 
    FROM target_table
);

-- WINDOW FUNCTIONS FOR ANALYTICS
SELECT 
    user_id,
    event_date,
    COUNT(*) OVER (
        PARTITION BY user_id 
        ORDER BY event_date 
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) as events_last_7_days
FROM user_events;
```

---

## 🧊 **ICEBERG INTEGRATION**

### **Python + Iceberg Patterns**
```python
# ICEBERG WITH PYSPARK
from pyspark.sql import SparkSession

# Initialize Spark with Iceberg
spark = SparkSession.builder \
    .appName("IcebergApp") \
    .config("spark.sql.extensions", 
            "org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions") \
    .config("spark.sql.catalog.spark_catalog", 
            "org.apache.iceberg.spark.SparkSessionCatalog") \
    .config("spark.sql.catalog.spark_catalog.type", "hive") \
    .getOrCreate()

# CREATE ICEBERG TABLE
def create_iceberg_table(table_name, schema):
    spark.sql(f"""
        CREATE TABLE {table_name} (
            {schema}
        ) USING iceberg
        PARTITIONED BY (days(event_time))
    """)

# MIGRATION PATTERN: DELTA TO ICEBERG
def migrate_delta_to_iceberg(delta_table_path, iceberg_table_name):
    # Read from Delta
    df = spark.read.format("delta").load(delta_table_path)
    
    # Write to Iceberg with proper partitioning
    df.write \
        .format("iceberg") \
        .mode("overwrite") \
        .option("write.format.default", "parquet") \
        .saveAsTable(iceberg_table_name)
    
    # Verify migration
    delta_count = spark.read.format("delta").load(delta_table_path).count()
    iceberg_count = spark.table(iceberg_table_name).count()
    
    assert delta_count == iceberg_count, f"Migration failed: {delta_count} != {iceberg_count}"

# ICEBERG TIME TRAVEL
def query_iceberg_history(table_name, timestamp):
    return spark.sql(f"""
        SELECT * FROM {table_name}
        TIMESTAMP AS OF '{timestamp}'
    """)

# SCHEMA EVOLUTION
def add_column_to_iceberg(table_name, column_name, column_type):
    spark.sql(f"""
        ALTER TABLE {table_name}
        ADD COLUMN {column_name} {column_type}
    """)
```

### **SQL + Iceberg Patterns**
```sql
-- CREATE ICEBERG TABLE
CREATE TABLE iceberg_catalog.sales.transactions (
    transaction_id STRING,
    user_id STRING,
    amount DECIMAL(10,2),
    transaction_date DATE,
    region STRING
) USING iceberg
PARTITIONED BY (region, bucket(10, user_id));

-- TIME TRAVEL QUERIES
SELECT * FROM iceberg_catalog.sales.transactions
TIMESTAMP AS OF '2024-01-01 00:00:00';

-- SCHEMA EVOLUTION
ALTER TABLE iceberg_catalog.sales.transactions
ADD COLUMN payment_method STRING;

-- PARTITION EVOLUTION
ALTER TABLE iceberg_catalog.sales.transactions
REPLACE PARTITION FIELD region WITH truncate(region, 2);

-- MIGRATION WITH VALIDATION
WITH source_data AS (
    SELECT * FROM delta_table
    WHERE updated_at > (
        SELECT COALESCE(MAX(updated_at), '1900-01-01')
        FROM iceberg_table
    )
)
INSERT INTO iceberg_table
SELECT * FROM source_data;

-- MULTI-FORMAT QUERYING
WITH iceberg_data AS (
    SELECT user_id, event_count
    FROM iceberg_catalog.events.user_events
),
delta_data AS (
    SELECT user_id, purchase_amount
    FROM delta.`/path/to/purchases`
)
SELECT 
    i.user_id,
    i.event_count,
    d.purchase_amount
FROM iceberg_data i
JOIN delta_data d ON i.user_id = d.user_id;

-- ICEBERG MAINTENANCE
-- Optimize file layout
CALL spark_catalog.system.rewrite_data_files('iceberg_catalog.db.table');

-- Remove old snapshots
CALL spark_catalog.system.expire_snapshots('iceberg_catalog.db.table', 
                                           TIMESTAMP '2024-01-01 00:00:00');

-- Update table statistics
CALL spark_catalog.system.rewrite_position_delete_files('iceberg_catalog.db.table');
```

### **Migration Expertise Patterns**
```python
# MIGRATION ASSESSMENT
class MigrationAssessment:
    def analyze_table(self, table_path):
        return {
            'size_gb': self._get_table_size(table_path),
            'row_count': self._get_row_count(table_path),
            'schema_complexity': self._assess_schema(table_path),
            'partition_strategy': self._analyze_partitions(table_path),
            'migration_time_estimate': self._estimate_time(table_path)
        }

# ZERO-DOWNTIME MIGRATION
class ZeroDowntimeMigration:
    def execute(self):
        self._setup_dual_write()        # Write to both formats
        self._backfill_historical()     # Copy existing data
        self._validate_consistency()    # Ensure data matches
        self._switch_reads()           # Start reading from Iceberg
        self._cleanup_source()         # Remove Delta table

# PERFORMANCE OPTIMIZATION
def optimize_iceberg_table(table_name):
    # Compact small files
    spark.sql(f"CALL spark_catalog.system.rewrite_data_files('{table_name}')")
    
    # Update statistics
    spark.sql(f"ANALYZE TABLE {table_name} COMPUTE STATISTICS")
    
    # Expire old snapshots
    spark.sql(f"""
        CALL spark_catalog.system.expire_snapshots(
            '{table_name}', 
            TIMESTAMP '{datetime.now() - timedelta(days=7)}'
        )
    """)
```

**Keep this file handy for quick reference during your learning journey!** 📚

**With Iceberg integration, you're positioned at the forefront of the data lakehouse evolution!** 🧊 