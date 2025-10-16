# Ride Sharing Analytics Using Spark Streaming and Spark SQL.
---
## **Prerequisites**
Before starting the assignment, ensure you have the following software installed and properly configured on your machine:
1. **Python 3.x**:
   - [Download and Install Python](https://www.python.org/downloads/)
   - Verify installation:
     ```bash
     python3 --version
     ```

2. **PySpark**:
   - Install using `pip`:
     ```bash
     pip install pyspark
     ```

3. **Faker**:
   - Install using `pip`:
     ```bash
     pip install faker
     ```

---

## **Setup Instructions**

### **1. Project Structure**

Ensure your project directory follows the structure below:

```
ride-sharing-analytics/
├── outputs/
│   ├── task_1
│   |    └── CSV files of task 1.
|   ├── task_2
│   |    └── CSV files of task 2.
|   └── task_3
│       └── CSV files of task 3.
├── task1.py
├── task2.py
├── task3.py
├── data_generator.py
└── README.md
```

- **data_generator.py/**: generates a constant stream of input data of the schema (trip_id, driver_id, distance_km, fare_amount, timestamp)  
- **outputs/**: CSV files of processed data of each task stored in respective folders.
- **README.md**: Assignment instructions and guidelines.
  
---

### **2. Running the Analysis Tasks**

You can run the analysis tasks either locally.

1. **Execute Each Task **: The data_generator.py should be continuosly running on a terminal. open a new terminal to execute each of the tasks.
   ```bash
     python data_generator.py
     python task1.py
     python task2.py
     python task3.py
   ```

2. **Verify the Outputs**:
   Check the `outputs/` directory for the resulting files:
   ```bash
   ls outputs/
   ```

---

## **Overview**

In this assignment, we will build a real-time analytics pipeline for a ride-sharing platform using Apache Spark Structured Streaming. we will process streaming data, perform real-time aggregations, and analyze trends over time.

## **Objectives**

By the end of this assignment, you should be able to:

1. Task 1: Ingest and parse real-time ride data.
2. Task 2: Perform real-time aggregations on driver earnings and trip distances.
3. Task 3: Analyze trends over time using a sliding time window.

---

## **Task 1: Basic Streaming Ingestion and Parsing**

1. Ingest streaming data from the provided socket (e.g., localhost:9999) using Spark Structured Streaming.
2. Parse the incoming JSON messages into a Spark DataFrame with proper columns (trip_id, driver_id, distance_km, fare_amount, timestamp).

## **Instructions:**
1. Create a Spark session.
2. Use spark.readStream.format("socket") to read from localhost:9999.
3. Parse the JSON payload into columns.
4. Print the parsed data to the console (using .writeStream.format("console")).

## **Output 1:**
```bash
2a97e74f-cff2-45f7-81a1-89fd60a968f7,56,1.7,120.68,2025-10-16 02:43:46

a8230b9b-dc72-4d7b-82ff-2295b2ddc3f4,4,4.2,68.23,2025-10-16 02:43:42
fe57e0f2-db31-405b-a9e5-7dbeb89fe430,78,25.34,100.33,2025-10-16 02:43:44
```

---

## **Task 2: Real-Time Aggregations (Driver-Level)**

1. Aggregate the data in real time to answer the following questions:
  • Total fare amount grouped by driver_id.
  • Average distance (distance_km) grouped by driver_id.
2. Output these aggregations to the console in real time.

## **Instructions:**
1. Reuse the parsed DataFrame from Task 1.
2. Group by driver_id and compute:
3. SUM(fare_amount) as total_fare
4. AVG(distance_km) as avg_distance
5. Store the result in csv

## **Output 2:**
```bash
driver_id,total_fare,avg_distance
7,81.39,41.48
54,44.28,6.09
29,130.76,38.33
42,31.36,26.22
87,103.9,15.21
73,127.33,31.78
64,148.68,43.08
3,99.21,27.96
34,205.6,35.39
59,51.31,28.75
22,20.72,14.22
85,114.59,22.92
71,10.81,19.11
98,203.76,32.53333333333334
47,41.01,6.75
96,90.44,28.78
43,201.95999999999998,32.685
61,277.22,15.155000000000001
27,64.23,26.13
75,146.24,4.14
26,69.01,27.22
78,31.97,2.69
77,156.94,46.394999999999996
89,51.6,27.47
19,79.16,16.96
55,125.58,10.84
93,83.33,46.84
95,106.62,23.49
38,96.3,47.67
92,74.97,30.52
58,55.08,31.16
33,106.71,13.07
97,29.17,45.99
84,404.01,21.07
79,82.82,8.18
24,54.34,44.19
88,107.16,48.14
56,188.72,26.22
4,85.16,37.51
39,113.67,17.98
62,164.92000000000002,27.31
13,14.44,25.03
66,70.4,20.73
91,130.16,32.5
72,8.34,36.42
45,129.44,29.47
```

---

## **Task 3: Windowed Time-Based Analytics**

1. Convert the timestamp column to a proper TimestampType.
2. Perform a 5-minute windowed aggregation on fare_amount (sliding by 1 minute and watermarking by 1 minute).

## **Instructions:**

1. Convert the string-based timestamp column to a TimestampType column (e.g., event_time).
2. Use Spark’s window function to aggregate over a 5-minute window, sliding by 1 minute, for the sum of fare_amount.
3. Output the windowed results to csv.

## **Output 3:**
```bash
window_start,window_end,sum_fare
2025-10-16T02:41:00.000Z,2025-10-16T02:46:00.000Z,2081.61
2025-10-16T02:42:00.000Z,2025-10-16T02:47:00.000Z,7172.3
```

---

## 📬 Submission Checklist

- [ ] Python scripts 
- [ ] Output files in the `outputs/` directory  
- [ ] Completed `README.md`  
- [ ] Commit everything to GitHub Classroom  
- [ ] Submit your GitHub repo link on canvas

---

