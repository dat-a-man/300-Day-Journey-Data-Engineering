# Python & SQL Foundation Roadmap (Beginner to Advanced)

## 🎯 **Learning Philosophy**
**Build a rock-solid foundation** with practical cheat sheets and notes that you can reference quickly. Focus on **data engineering-specific patterns** that you'll use daily.

## 📚 **Learning Progression**

### **Phase 1: Python Fundamentals (Weeks 1-4)**
**Goal**: From beginner to intermediate Python for data engineering

### **Phase 2: SQL Mastery (Weeks 5-8)**
**Goal**: From basic queries to advanced analytics and optimization

### **Phase 3: Data Engineering Integration (Weeks 9-12)**
**Goal**: Combine Python + SQL for real data engineering workflows

---

## 🐍 **PHASE 1: Python Fundamentals (Weeks 1-4)**

### **Week 1: Python Basics & Data Types**
**Daily Focus (30 minutes each):**

#### **Day 1-2: Variables, Data Types, Basic Operations**
**Learning Resources:**
- [Python for Data Analysis (Chapters 1-2)](https://wesmckinney.com/book/) - 45 min
- [Real Python: Variables](https://realpython.com/python-variables/) - 20 min

**Cheat Sheet:**
```python
# VARIABLES & DATA TYPES
name = "Aman"                    # str
age = 28                         # int
salary = 75000.50                # float
is_remote = True                 # bool
skills = ["Python", "SQL"]       # list
experience = {"years": 3}        # dict

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

**Doable Action**: Create a simple data engineer profile script

#### **Day 3-4: Control Flow (if/else, loops)**
**Learning Resources:**
- [Python Control Flow](https://realpython.com/python-conditional-statements/) - 30 min
- [Python Loops](https://realpython.com/python-for-loop/) - 30 min

**Cheat Sheet:**
```python
# IF/ELSE STATEMENTS
age = 25
if age >= 18:
    status = "adult"
elif age >= 13:
    status = "teenager"
else:
    status = "child"

# FOR LOOPS
skills = ["Python", "SQL", "Databricks"]
for skill in skills:
    print(f"I know {skill}")

# LIST COMPREHENSIONS (DATA ENGINEERING ESSENTIAL)
numbers = [1, 2, 3, 4, 5]
squares = [x**2 for x in numbers]        # [1, 4, 9, 16, 25]
evens = [x for x in numbers if x % 2 == 0]  # [2, 4]

# WHILE LOOPS
count = 0
while count < 5:
    print(count)
    count += 1
```

**Doable Action**: Build a data quality checker script

#### **Day 5-7: Functions & Error Handling**
**Learning Resources:**
- [Python Functions](https://realpython.com/defining-your-own-python-function/) - 40 min
- [Python Exceptions](https://realpython.com/python-exceptions/) - 35 min

**Cheat Sheet:**
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

**Doable Action**: Create reusable data processing functions

### **Week 2: Data Structures & File Operations**

#### **Day 8-10: Lists, Dictionaries, Sets**
**Learning Resources:**
- [Python Data Structures](https://realpython.com/python-data-structures/) - 45 min
- [Python Dictionaries](https://realpython.com/python-dicts/) - 30 min

**Cheat Sheet:**
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

# DATA ENGINEERING PATTERN: CONFIGURATION MANAGEMENT
def get_database_config(environment="dev"):
    configs = {
        "dev": {"host": "localhost", "port": 5432},
        "prod": {"host": "prod-db.com", "port": 5432}
    }
    return configs.get(environment, configs["dev"])
```

#### **Day 11-14: File Operations & JSON/CSV**
**Learning Resources:**
- [Python File Operations](https://realpython.com/read-write-files-python/) - 30 min
- [Working with JSON](https://realpython.com/python-json/) - 25 min
- [CSV Processing](https://realpython.com/python-csv/) - 25 min

**Cheat Sheet:**
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

# DATA ENGINEERING PATTERN: CONFIG FILE LOADING
def load_config(config_path):
    try:
        with open(config_path, 'r') as file:
            return json.load(file)
    except FileNotFoundError:
        print(f"Config file {config_path} not found")
        return {}
```

### **Week 3: Advanced Python for Data Engineering**

#### **Day 15-17: Object-Oriented Programming Basics**
**Learning Resources:**
- [Python OOP](https://realpython.com/python3-object-oriented-programming/) - 45 min

**Cheat Sheet:**
```python
# CLASS DEFINITION
class DataPipeline:
    def __init__(self, name, source, destination):
        self.name = name
        self.source = source
        self.destination = destination
        self.status = "idle"
    
    def run(self):
        self.status = "running"
        print(f"Running pipeline: {self.name}")
        # pipeline logic here
        self.status = "completed"
    
    def get_status(self):
        return f"{self.name}: {self.status}"

# USAGE
pipeline = DataPipeline("user_data", "database", "warehouse")
pipeline.run()
print(pipeline.get_status())
```

#### **Day 18-21: Modules, Packages, Virtual Environments**
**Learning Resources:**
- [Python Modules](https://realpython.com/python-modules-packages/) - 30 min
- [Virtual Environments](https://realpython.com/python-virtual-environments-a-primer/) - 25 min

**Cheat Sheet:**
```python
# MODULE IMPORTS
import pandas as pd
import numpy as np
from datetime import datetime
from typing import List, Dict, Optional

# VIRTUAL ENVIRONMENT SETUP
# python -m venv data_engineering_env
# source data_engineering_env/bin/activate  # Linux/Mac
# data_engineering_env\Scripts\activate     # Windows

# REQUIREMENTS.TXT
# pandas==2.0.0
# numpy==1.24.0
# requests==2.28.0

# DATA ENGINEERING PATTERN: UTILITY MODULE
# utils.py
import logging
from typing import Dict, Any

def setup_logging(level="INFO"):
    logging.basicConfig(level=getattr(logging, level))
    return logging.getLogger(__name__)

def validate_config(config: Dict[str, Any]) -> bool:
    required_keys = ["database", "host", "port"]
    return all(key in config for key in required_keys)
```

### **Week 4: Python Data Engineering Patterns**

#### **Day 22-28: Data Processing Patterns**
**Learning Resources:**
- [Python Data Processing](https://realpython.com/python-data-processing/) - 40 min

**Cheat Sheet:**
```python
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

# CONFIGURATION PATTERN
class DataConfig:
    def __init__(self):
        self.database_url = os.getenv('DATABASE_URL', 'localhost')
        self.batch_size = int(os.getenv('BATCH_SIZE', '1000'))
        self.retry_attempts = int(os.getenv('RETRY_ATTEMPTS', '3'))

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

## 🗄️ **PHASE 2: SQL Mastery (Weeks 5-8)**

### **Week 5: SQL Fundamentals**

#### **Day 29-31: Basic Queries & SELECT**
**Learning Resources:**
- [SQL Basics](https://www.sqlbolt.com/) - 30 min
- [SELECT Queries](https://www.w3schools.com/sql/sql_select.asp) - 25 min

**Cheat Sheet:**
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

#### **Day 32-35: WHERE, ORDER BY, Aggregations**
**Learning Resources:**
- [SQL WHERE](https://www.w3schools.com/sql/sql_where.asp) - 20 min
- [SQL Aggregations](https://www.w3schools.com/sql/sql_count_avg_sum.asp) - 30 min

**Cheat Sheet:**
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

### **Week 6: Advanced SQL Queries**

#### **Day 36-38: JOINs**
**Learning Resources:**
- [SQL JOINs](https://www.w3schools.com/sql/sql_join.asp) - 35 min

**Cheat Sheet:**
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

-- DATA ENGINEERING PATTERN: DATA RECONCILIATION
SELECT 
    'Missing in orders' as issue_type,
    u.user_id,
    u.name
FROM users u
LEFT JOIN orders o ON u.user_id = o.user_id
WHERE o.order_id IS NULL
UNION ALL
SELECT 
    'Orphaned order' as issue_type,
    o.user_id,
    'Unknown' as name
FROM orders o
LEFT JOIN users u ON o.user_id = u.user_id
WHERE u.user_id IS NULL;
```

#### **Day 39-42: Subqueries & CTEs**
**Learning Resources:**
- [SQL Subqueries](https://www.w3schools.com/sql/sql_subqueries.asp) - 30 min
- [SQL CTEs](https://www.w3schools.com/sql/sql_cte.asp) - 25 min

**Cheat Sheet:**
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

-- DATA ENGINEERING PATTERN: HIERARCHICAL DATA
WITH RECURSIVE org_hierarchy AS (
    -- Base case: top level employees
    SELECT 
        employee_id,
        name,
        manager_id,
        1 as level
    FROM employees
    WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Recursive case: subordinates
    SELECT 
        e.employee_id,
        e.name,
        e.manager_id,
        oh.level + 1
    FROM employees e
    JOIN org_hierarchy oh ON e.manager_id = oh.employee_id
)
SELECT * FROM org_hierarchy ORDER BY level, name;
```

### **Week 7: SQL Performance & Optimization**

#### **Day 43-45: Window Functions**
**Learning Resources:**
- [SQL Window Functions](https://www.postgresql.org/docs/current/tutorial-window.html) - 35 min

**Cheat Sheet:**
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

#### **Day 46-49: Performance Optimization**
**Learning Resources:**
- [SQL Performance](https://use-the-index-luke.com/) - 40 min

**Cheat Sheet:**
```sql
-- EXPLAIN PLAN (UNDERSTAND QUERY PERFORMANCE)
EXPLAIN ANALYZE 
SELECT * FROM users WHERE email = 'user@example.com';

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

### **Week 8: Advanced SQL Patterns**

#### **Day 50-56: Data Engineering SQL Patterns**
**Learning Resources:**
- [SQL for Data Engineering](https://www.datacamp.com/courses/intro-to-sql-for-data-science) - 45 min

**Cheat Sheet:**
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

-- DATA LINEAGE TRACKING
CREATE TABLE data_lineage (
    table_name VARCHAR(100),
    source_table VARCHAR(100),
    transformation_type VARCHAR(50),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

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

## 🔗 **PHASE 3: Data Engineering Integration (Weeks 9-12)**

### **Week 9-10: Python + SQL Integration**

#### **Day 57-70: Database Connectivity & ORMs**
**Learning Resources:**
- [SQLAlchemy Tutorial](https://docs.sqlalchemy.org/en/14/tutorial/) - 45 min
- [psycopg2 Documentation](https://www.psycopg.org/docs/) - 30 min

**Cheat Sheet:**
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

### **Week 11-12: Production-Ready Data Engineering**

#### **Day 71-84: Error Handling, Logging, Monitoring**
**Cheat Sheet:**
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

## 📋 **QUICK REFERENCE CHEAT SHEETS**

### **Python Data Engineering Quick Reference**
```python
# ESSENTIAL IMPORTS
import pandas as pd
import numpy as np
from datetime import datetime, timedelta
import logging
from typing import List, Dict, Optional, Any
import json
import csv
import os

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

## 🎯 **Success Metrics**

### **Week 4 Targets:**
- [ ] Write Python functions for data validation
- [ ] Create reusable data processing modules
- [ ] Handle errors gracefully in data operations
- [ ] Build simple data pipeline class

### **Week 8 Targets:**
- [ ] Write complex SQL queries with JOINs and CTEs
- [ ] Optimize SQL queries for performance
- [ ] Implement data quality checks in SQL
- [ ] Use window functions for analytics

### **Week 12 Targets:**
- [ ] Integrate Python and SQL in data pipelines
- [ ] Implement comprehensive error handling
- [ ] Create production-ready data validation
- [ ] Build configurable data processing framework

**This foundation will make you confident in both Python and SQL for data engineering, with practical cheat sheets you can reference quickly!** 