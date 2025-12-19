# BigData

# 🐘 Big Data Labs - Hướng dẫn Chi tiết từ A đến Z

> **Dự án thực hành đầy đủ** về xử lý dữ liệu lớn (Big Data) với Hadoop HDFS, MapReduce, Apache Spark, Spark Streaming và ElasticSearch - Tất cả chạy trên Docker.

[![Hadoop](https://img.shields.io/badge/Hadoop-3.2.1-yellow?logo=apache-hadoop)](https://hadoop.apache.org/)
[![Spark](https://img.shields.io/badge/Spark-3.1.1-orange?logo=apache-spark)](https://spark.apache.org/)
[![ElasticSearch](https://img.shields.io/badge/ElasticSearch-7.15.2-blue?logo=elasticsearch)](https://www.elastic.co/)
[![Docker](https://img.shields.io/badge/Docker-Required-blue?logo=docker)](https://www.docker.com/)

**📌 Hướng dẫn này được viết CHI TIẾT để bạn hiểu và làm theo từng bước một cách DỄ DÀNG NHẤT!**

---

## 📖 Mục lục

- [Giới thiệu](#-giới-thiệu)
- [Kiến trúc hệ thống](#-kiến-trúc-hệ-thống)
- [Công nghệ sử dụng](#️-công-nghệ-sử-dụng)
- [Yêu cầu hệ thống](#-yêu-cầu-hệ-thống)
- [Cài đặt và khởi động](#-cài-đặt-và-khởi-động)
- [Chi tiết các Labs](#-chi-tiết-các-labs)
- [Hướng dẫn sử dụng](#-hướng-dẫn-sử-dụng)
- [Web UIs & Monitoring](#-web-uis--monitoring)
- [Troubleshooting](#️-troubleshooting)
- [Best Practices](#-best-practices)
- [Tài liệu tham khảo](#-tài-liệu-tham-khảo)

---

## 🎯 Giới thiệu

Dự án này cung cấp một **môi trường Big Data hoàn chỉnh** được containerized với Docker, bao gồm:

- **Hadoop Distributed File System (HDFS)** - Lưu trữ phân tán
- **YARN** - Resource management và job scheduling
- **MapReduce** - Xử lý dữ liệu batch song song
- **Apache Spark** - Xử lý dữ liệu nhanh in-memory
- **Spark Streaming** - Xử lý dữ liệu real-time
- **ElasticSearch** - Full-text search và analytics
- **Kibana** - Data visualization

### 🎓 Mục đích học tập

1. **Lab 1**: Hiểu về HDFS và lưu trữ phân tán
2. **Lab 2**: Lập trình MapReduce với Java
3. **Lab 3**: Tìm kiếm và phân tích với ElasticSearch
4. **Lab 4**: Xử lý dữ liệu nhanh với Apache Spark
5. **Lab 5**: Real-time processing với Spark Streaming

---

## 🏗️ Kiến trúc hệ thống

```
┌─────────────────────────────────────────────────────────────┐
│                     CLIENT APPLICATIONS                      │
│          (Web UIs, Scripts, Python/Java Programs)            │
└───────────────────────┬─────────────────────────────────────┘
                        │
        ┌───────────────┴───────────────┐
        │                               │
┌───────▼──────┐              ┌────────▼────────┐
│  PROCESSING  │              │   SEARCH &      │
│   ENGINES    │              │   ANALYTICS     │
├──────────────┤              ├─────────────────┤
│ MapReduce    │              │ ElasticSearch   │
│ Apache Spark │              │ Kibana          │
│ Spark Stream │              └────────┬────────┘
└───────┬──────┘                       │
        │                              │
        │         ┌────────────────────┘
        │         │
┌───────▼─────────▼───────────────────────────────────┐
│           HADOOP DISTRIBUTED FILE SYSTEM             │
│                      (HDFS)                          │
├──────────────────────────────────────────────────────┤
│  NameNode  │  DataNode 1  │  DataNode 2             │
│  (Master)  │   (Worker)   │   (Worker)              │
└──────────────────────────────────────────────────────┘
                        │
        ┌───────────────┴───────────────┐
        │                               │
┌───────▼──────┐              ┌────────▼────────┐
│ YARN Resource│              │  Spark Cluster  │
│   Manager    │              │                 │
│              │              │ Master + Worker │
└──────────────┘              └─────────────────┘
```

---

## 🛠️ Công nghệ sử dụng

### Core Technologies

| Công nghệ | Version | Mục đích | Port |
|-----------|---------|----------|------|
| **Hadoop HDFS** | 3.2.1 | Distributed file storage | 9870 |
| **YARN** | 3.2.1 | Resource management | 8088 |
| **Apache Spark** | 3.1.1 | Fast data processing | 8082 |
| **ElasticSearch** | 7.15.2 | Search & analytics | 9200 |
| **Kibana** | 7.15.2 | Data visualization | 5601 |
| **Docker** | Latest | Containerization | - |

### Programming Languages

- **Java** - MapReduce jobs
- **Python** - Spark jobs (PySpark)
- **Scala** - Spark Streaming jobs

---

## 📋 Yêu cầu hệ thống

### Phần cứng

| Thành phần | Tối thiểu | Khuyến nghị |
|------------|-----------|-------------|
| **RAM** | 8 GB | 16 GB |
| **CPU** | 4 cores | 8 cores |
| **Disk** | 20 GB trống | 50 GB |
| **Network** | Internet connection | High-speed |

### Phần mềm

- **OS**: Windows 10/11, macOS, hoặc Linux
- **Docker Desktop**: Version 20.10+
- **PowerShell**: Version 5.1+ (Windows)
- **Git**: Optional, để clone repository

---

## 🚀 Cài đặt và khởi động

### Bước 1: Cài đặt Docker Desktop

1. Download Docker Desktop:
   - Windows: https://www.docker.com/products/docker-desktop
   - macOS: https://docs.docker.com/desktop/mac/install/
   - Linux: https://docs.docker.com/engine/install/

2. Cấu hình Docker Desktop:
   ```
   Settings → Resources → Memory: 8GB (khuyến nghị 12GB)
   Settings → Resources → CPU: 4 cores (khuyến nghị 6 cores)
   Settings → Resources → Disk: 20GB
   ```

3. Khởi động Docker Desktop và đảm bảo nó đang chạy

### Bước 2: Clone hoặc Download Project

```powershell
# Option 1: Clone từ Git (nếu có)
git clone <repository-url>
cd "Bai Lab 1.2.3.4.5"

# Option 2: Download và giải nén
# Sau đó mở PowerShell tại thư mục project
```

### Bước 3: Setup môi trường

```powershell
# Chạy script setup tự động
.\setup.ps1
```

Script `setup.ps1` sẽ thực hiện:
- ✅ Kiểm tra Docker đang chạy
- ✅ Pull các Docker images (lần đầu ~5-10GB)
- ✅ Khởi động toàn bộ cluster
- ✅ Tạo thư mục HDFS cần thiết
- ✅ Upload dữ liệu mẫu lên HDFS

**⏱️ Lưu ý**: Lần đầu tiên sẽ mất 10-15 phút để download images.

### Bước 4: Kiểm tra cài đặt

Mở trình duyệt và kiểm tra các Web UIs:

```
✓ HDFS NameNode:        http://localhost:9870
✓ YARN ResourceManager: http://localhost:8088
✓ Spark Master:         http://localhost:8082
✓ Spark Worker:         http://localhost:8083
```

Kiểm tra containers đang chạy:

```powershell
docker-compose ps
```

Bạn sẽ thấy:
- ✅ namenode
- ✅ datanode1, datanode2
- ✅ resourcemanager
- ✅ nodemanager
- ✅ historyserver
- ✅ spark-master
- ✅ spark-worker-1

---

## 📚 Chi tiết các Labs

### 🔵 Lab 1: Hadoop HDFS - Distributed File System

**Mục tiêu**: Hiểu cách HDFS lưu trữ và phân tán dữ liệu

**Nội dung**:
- Kiến trúc HDFS (NameNode + DataNodes)
- Replication và fault tolerance
- Block storage (mặc định 128MB/block)
- Upload file lớn (1GB) và quan sát phân tán

**Các bước thực hành**:

1. **Khởi động HDFS cluster**:
   ```powershell
   docker-compose up -d namenode datanode1 datanode2
   ```

2. **Tạo thư mục trong HDFS**:
   ```powershell
   docker exec namenode hdfs dfs -mkdir -p /user/hadoop
   ```

3. **Upload file 1GB**:
   ```powershell
   docker exec namenode hdfs dfs -put Lab01/1GB/1GB.bin /user/hadoop/hdsd/data.bin
   ```

4. **Kiểm tra phân tán blocks**:
   ```powershell
   docker exec namenode hdfs fsck /user/hadoop/hdsd/data.bin -files -blocks -locations
   ```

**Kết quả mong đợi**:
- File 1GB được chia thành 8 blocks (~128MB/block)
- Mỗi block được replicate 2 lần (vì có 2 datanodes)
- Web UI hiển thị: http://localhost:9870

---

### 🟢 Lab 2: Hadoop MapReduce - Word Count

**Mục tiêu**: Lập trình MapReduce với Java để xử lý dữ liệu lớn

**Nội dung**:
- MapReduce paradigm (Map → Shuffle → Reduce)
- Viết Mapper và Reducer với Java
- Compile và đóng gói JAR
- Chạy job trên YARN cluster

**Source Code**: `Lab02/WordCount/src/WordCount.java`

**Kiến trúc MapReduce**:
```
Input File (HDFS)
     ↓
  Mapper (split & emit)
     ↓
  Shuffle & Sort
     ↓
  Reducer (aggregate)
     ↓
Output File (HDFS)
```

**Chạy Lab 2**:

```powershell
.\run-lab2.ps1
```

Hoặc thủ công:

```powershell
# 1. Upload input file lên HDFS
docker exec namenode hdfs dfs -put Lab02/input_test.txt /user/hadoop/input/

# 2. Chạy MapReduce job
docker exec namenode hadoop jar /workspace/Lab02/wchdsd.jar WordCount /user/hadoop/input /user/hadoop/wordcount/output

# 3. Xem kết quả
docker exec namenode hdfs dfs -cat /user/hadoop/wordcount/output/part-r-00000
```

**Giải thích code**:

```java
// Mapper: Tách từ và emit (word, 1)
public void map(Object key, Text value, Context context) {
    StringTokenizer itr = new StringTokenizer(value.toString());
    while (itr.hasMoreTokens()) {
        word.set(itr.nextToken());
        context.write(word, one);  // emit (word, 1)
    }
}

// Reducer: Tổng hợp count
public void reduce(Text key, Iterable<IntWritable> values, Context context) {
    int sum = 0;
    for (IntWritable val : values) {
        sum += val.get();
    }
    result.set(sum);
    context.write(key, result);  // emit (word, total_count)
}
```

**Monitoring**:
- YARN UI: http://localhost:8088
- Job history: http://localhost:19888

---

### 🔴 Lab 3: ElasticSearch & Kibana - Search Engine

**Mục tiêu**: Xây dựng hệ thống tìm kiếm và phân tích dữ liệu

**Nội dung**:
- ElasticSearch cluster (1 master + 2 data nodes)
- Indexing và searching
- Sharding và replication
- Kibana visualization

**Khởi động Lab 3**:

```powershell
.\run-lab3.ps1
# hoặc
docker-compose --profile lab3 up -d
```

**Các thành phần**:
- `elasticsearch-master`: Master node (không lưu data)
- `elasticsearch-data1`: Data node 1
- `elasticsearch-data2`: Data node 2
- `kibana`: Web UI

**Thao tác cơ bản**:

```powershell
# 1. Kiểm tra cluster health
Invoke-RestMethod -Uri "http://localhost:9200/_cluster/health?pretty"

# 2. Tạo index và thêm document
$data = @{
    title = "Big Data Lab"
    content = "Learning Hadoop and Spark"
} | ConvertTo-Json

Invoke-RestMethod -Uri "http://localhost:9200/test-index/_doc/1" -Method Put -Body $data -ContentType "application/json"

# 3. Search
Invoke-RestMethod -Uri "http://localhost:9200/test-index/_search?q=Hadoop"

# 4. Xem shard distribution
Invoke-RestMethod -Uri "http://localhost:9200/_cat/shards/test-index?v"
```

**Web UIs**:
- ElasticSearch: http://localhost:9200
- Kibana: http://localhost:5601

**Kibana Dev Tools Console**:
```json
GET _cluster/health
GET _cat/nodes?v
GET test-index/_search
```

---

### 🟡 Lab 4: Apache Spark - Fast Data Processing

**Mục tiêu**: Xử lý dữ liệu nhanh hơn MapReduce 10-100 lần

**Nội dung**:
- RDD (Resilient Distributed Dataset)
- Transformations và Actions
- In-memory computing
- PySpark programming

**Chương trình**:

1. **WordCount.py**: Word count cơ bản
2. **SparkWordCount.py**: Word count nâng cao với threshold

**Chạy Lab 4**:

```powershell
.\run-lab4.ps1
```

Hoặc thủ công:

```powershell
# Chạy WordCount.py
docker exec spark-master spark-submit \
  --master local[*] \
  /workspace/Lab04/WordCount.py \
  hdfs://namenode:9000/user/hadoop/input/input_test.txt \
  hdfs://namenode:9000/user/hadoop/spark-output

# Xem kết quả
docker exec namenode hdfs dfs -cat /user/hadoop/spark-output/part-*
```

**So sánh Spark vs MapReduce**:

| Feature | MapReduce | Spark |
|---------|-----------|-------|
| **Speed** | Baseline | 10-100x nhanh hơn |
| **Storage** | Disk-based | In-memory |
| **API** | Java complex | Python/Scala simple |
| **Use case** | Batch processing | Batch + Streaming + ML |

**Code example (PySpark)**:

```python
from pyspark import SparkContext

sc = SparkContext("local", "WordCount")

# Read từ HDFS
text_file = sc.textFile("hdfs://namenode:9000/user/hadoop/input/input.txt")

# Map-Reduce với Spark
counts = text_file.flatMap(lambda line: line.split(" ")) \
                  .map(lambda word: (word, 1)) \
                  .reduceByKey(lambda a, b: a + b)

# Save kết quả
counts.saveAsTextFile("hdfs://namenode:9000/user/hadoop/output")
```

**Monitoring**:
- Spark Master UI: http://localhost:8082
- Spark Application UI: http://localhost:4040 (khi job chạy)

---

### 🟣 Lab 5: Spark Streaming - Real-time Processing

**Mục tiêu**: Xử lý dữ liệu real-time với window operations

**Nội dung**:
- DStream (Discretized Stream)
- Window operations (30s window, 10s slide)
- Apache log analysis
- Socket streaming

**Chương trình**:

1. **SocketStream.scala**: Stream cơ bản, lọc "error"
2. **LogAnalyzerStreaming.scala**: Phân tích Apache access logs

**Chạy Lab 5** (cần 2 terminals):

**Terminal 1** - Start Spark Streaming:
```powershell
.\run-lab5.ps1
# Chọn program (1 hoặc 2)
```

**Terminal 2** - Stream data vào port:
```powershell
# Stream log file
docker exec spark-master bash /workspace/Lab05/stream.sh
```

**Window Operations**:

```scala
val windowedCounts = lines
  .window(Seconds(30), Seconds(10))  // 30s window, slide 10s
  .flatMap(_.split(" "))
  .map(word => (word, 1))
  .reduceByKey(_ + _)
```

**Apache Log Analysis**:

Phân tích real-time:
- Response code distribution (200, 404, 500...)
- Content size statistics
- Top 10 endpoints
- Frequent IP addresses

**Monitoring**:
- Spark Streaming UI: http://localhost:4040

---

## 📖 Hướng dẫn sử dụng

### Quản lý Cluster

```powershell
# Xem trạng thái containers
docker-compose ps

# Khởi động toàn bộ cluster
docker-compose up -d

# Dừng cluster
docker-compose down

# Dừng và xóa volumes (XÓA DATA)
docker-compose down -v

# Restart một service
docker-compose restart namenode

# Xem logs
docker-compose logs -f namenode
docker-compose logs -f spark-master

# Xem resource usage
docker stats
```

### Làm việc với HDFS

```powershell
# Vào container namenode
docker exec -it namenode bash

# HDFS commands (trong container)
hdfs dfs -ls /                          # List root
hdfs dfs -ls /user/hadoop              # List directory
hdfs dfs -mkdir -p /user/hadoop/test   # Create directory
hdfs dfs -put local.txt /user/hadoop/  # Upload file
hdfs dfs -get /user/hadoop/file.txt ./ # Download file
hdfs dfs -cat /user/hadoop/file.txt    # View file
hdfs dfs -rm /user/hadoop/file.txt     # Delete file
hdfs dfs -rm -r /user/hadoop/dir       # Delete directory

# HDFS admin
hdfs dfsadmin -report                  # Cluster report
hdfs fsck / -files -blocks -locations  # File system check
```

### Làm việc với Spark

```powershell
# Vào Spark master container
docker exec -it spark-master bash

# Spark shell (Scala)
spark-shell --master local[*]

# PySpark shell
pyspark --master local[*]

# Submit Spark job
spark-submit \
  --master local[*] \
  --executor-memory 2g \
  --total-executor-cores 4 \
  your-script.py

# Submit với HDFS
spark-submit \
  --master local[*] \
  your-script.py \
  hdfs://namenode:9000/input \
  hdfs://namenode:9000/output
```

### Làm việc với ElasticSearch

```powershell
# REST API examples

# Cluster health
Invoke-RestMethod http://localhost:9200/_cluster/health?pretty

# List nodes
Invoke-RestMethod http://localhost:9200/_cat/nodes?v

# List indices
Invoke-RestMethod http://localhost:9200/_cat/indices?v

# Create index
Invoke-RestMethod -Method Put http://localhost:9200/my-index

# Add document
$doc = @{ title="Test"; content="Hello" } | ConvertTo-Json
Invoke-RestMethod -Method Post -Uri http://localhost:9200/my-index/_doc -Body $doc -ContentType "application/json"

# Search
Invoke-RestMethod http://localhost:9200/my-index/_search?q=Hello
```

---

## 🖥️ Web UIs & Monitoring

### Hadoop Ecosystem

| Service | URL | Mô tả |
|---------|-----|-------|
| **HDFS NameNode** | http://localhost:9870 | Browse HDFS, xem datanodes, blocks |
| **YARN ResourceManager** | http://localhost:8088 | Xem jobs, applications, cluster metrics |
| **Spark Master** | http://localhost:8082 | Xem workers, running applications |
| **Spark Worker** | http://localhost:8083 | Worker details, executor info |
| **Spark Application** | http://localhost:4040 | Job details (chỉ khi job chạy) |
| **Job History** | http://localhost:19888 | YARN job history |

### ElasticSearch Stack

| Service | URL | Mô tả |
|---------|-----|-------|
| **ElasticSearch** | http://localhost:9200 | REST API endpoint |
| **Kibana** | http://localhost:5601 | Data exploration & visualization |

### Monitoring từ Command Line

```powershell
# Container resources
docker stats

# HDFS cluster report
docker exec namenode hdfs dfsadmin -report

# YARN applications
docker exec resourcemanager yarn application -list

# Spark applications
docker exec spark-master curl http://localhost:8080/json/
```

---

## ⚠️ Troubleshooting

### Problem 1: Docker không khởi động

**Triệu chứng**: `docker-compose up` failed

**Giải pháp**:
```powershell
# Kiểm tra Docker Desktop đang chạy
Get-Process "Docker Desktop"

# Restart Docker Desktop
# Hoặc từ UI: Right-click Docker icon → Restart
```

### Problem 2: Containers không healthy

**Triệu chứng**: Container status = "unhealthy"

**Giải pháp**:
```powershell
# Xem logs
docker-compose logs namenode

# Restart container
docker-compose restart namenode

# Nếu vẫn lỗi, restart toàn bộ
docker-compose down
docker-compose up -d
```

### Problem 3: Out of memory

**Triệu chứng**: Container bị kill, application failed

**Giải pháp**:

1. Tăng memory cho Docker Desktop:
   - Settings → Resources → Memory → 12GB
   - Apply & Restart

2. Giảm resource requirements trong `docker-compose.yml`:
   ```yaml
   spark-worker-1:
     environment:
       - SPARK_WORKER_MEMORY=2g  # Giảm từ 4g
   ```

3. Giảm memory cho ElasticSearch:
   ```yaml
   elasticsearch-master:
     environment:
       - "ES_JAVA_OPTS=-Xms512m -Xmx512m"  # Giảm từ 2g
   ```

### Problem 4: Port đã được sử dụng

**Triệu chứng**: `port is already allocated`

**Giải pháp**:

Sửa `docker-compose.yml`, đổi port bên trái:
```yaml
ports:
  - "19870:9870"  # Thay vì 9870:9870
```

Hoặc tìm và kill process đang dùng port:
```powershell
# Tìm process
netstat -ano | findstr :9870

# Kill process
taskkill /PID <PID> /F
```

### Problem 5: HDFS không accessible

**Triệu chứng**: `hdfs dfs` commands fail

**Giải pháp**:
```powershell
# Kiểm tra namenode
docker exec namenode hdfs dfsadmin -report

# Nếu cần, format namenode (XÓA DATA!)
docker exec namenode hdfs namenode -format

# Restart HDFS
docker-compose restart namenode datanode1 datanode2
```

### Problem 6: ElasticSearch slow startup

**Triệu chứng**: Cluster không green sau vài phút

**Giải pháp**:

Đã được tối ưu trong config hiện tại:
- Memory: 512MB/node (thay vì 2GB)
- `bootstrap.memory_lock=false`
- Startup time: ~20-30 giây

Nếu vẫn chậm:
```powershell
# Xem logs
docker logs elasticsearch-master

# Restart
docker-compose --profile lab3 restart
```

### Problem 7: Spark job failed

**Triệu chứng**: Job crash hoặc stuck

**Giải pháp**:
```powershell
# Xem logs
docker exec spark-master cat /spark/logs/*

# Kiểm tra Spark UI
# http://localhost:8082

# Kiểm tra HDFS connection
docker exec spark-master hdfs dfs -ls /

# Restart Spark
docker-compose restart spark-master spark-worker-1
```

---

## 💡 Best Practices

### 1. Resource Management

- Đóng các applications không dùng để tiết kiệm RAM
- Sử dụng `docker stats` để monitor resource usage
- Dừng cluster khi không dùng: `docker-compose down`

### 2. Data Management

- Backup data quan trọng trước khi `docker-compose down -v`
- Sử dụng HDFS replication để đảm bảo data safety
- Clean up HDFS thường xuyên: `hdfs dfs -rm -r /user/hadoop/old-data`

### 3. Development Workflow

```powershell
# 1. Start cluster
docker-compose up -d

# 2. Develop & test locally
# Edit code trong Lab02/, Lab04/, Lab05/

# 3. Upload to HDFS (nếu cần)
docker exec namenode hdfs dfs -put local-file.txt /user/hadoop/

# 4. Run job
.\run-lab2.ps1  # hoặc lab4, lab5

# 5. Check results
docker exec namenode hdfs dfs -cat /user/hadoop/output/part-*

# 6. Stop cluster when done
docker-compose down
```

### 4. Debugging

- Luôn check logs: `docker-compose logs -f <service>`
- Sử dụng Web UIs để monitor
- Test với small dataset trước
- Verify HDFS data trước khi chạy job

---

## 📂 Cấu trúc Project

```
Bai Lab 1.2.3.4.5/
│
├── docker-compose.yml       # Main cluster configuration
├── hadoop.env               # Hadoop environment variables
├── setup.ps1                # Auto setup script
├── run-lab2.ps1            # Run MapReduce job
├── run-lab3.ps1            # Run ElasticSearch
├── run-lab4.ps1            # Run Spark job
├── run-lab5.ps1            # Run Spark Streaming
├── fix-docker.ps1          # Docker troubleshooting
│
├── Lab01/                   # HDFS Lab
│   ├── 1GB/
│   │   └── 1GB.bin         # 1GB sample file
│   └── Lab1.pdf            # Lab instructions
│
├── Lab02/                   # MapReduce Lab
│   ├── WordCount/
│   │   ├── src/
│   │   │   └── WordCount.java
│   │   ├── bin/            # Compiled classes
│   │   └── lib/            # Dependencies
│   ├── wchdsd.jar          # Compiled JAR
│   ├── input*.txt          # Input files
│   └── Lab2.pdf
│
├── Lab03/                   # ElasticSearch Lab
│   └── Lab3.pdf
│
├── Lab04/                   # Spark Lab
│   ├── WordCount.py        # Basic word count
│   ├── SparkWordCount.py   # Advanced word count
│   ├── WordCount_Local.py  # Local mode
│   ├── input/              # Test inputs
│   └── Lab4.pdf
│
├── Lab05/                   # Spark Streaming Lab
│   ├── SocketStream.scala
│   ├── LogAnalyzerStreaming.scala
│   ├── ApacheAccessLog.scala
│   ├── build.sbt           # SBT build file
│   ├── log.txt             # Sample Apache logs
│   ├── stream.sh           # Data streaming script
│   ├── Lab5.pdf
│   └── Run.txt
│
├── data/                    # Sample datasets
│   ├── coinmarket_alltime_1.csv
│   ├── coinmarket_alltime_2.csv
│   ├── coinmarket_alltime_3.csv
│   ├── coinmarket_alltime_4.csv
│   └── data.csv
│
└── README.md               # This file
```

---

## 📖 Tài liệu tham khảo

### Official Documentation

- [Apache Hadoop](https://hadoop.apache.org/docs/stable/)
- [Apache Spark](https://spark.apache.org/docs/latest/)
- [Apache Spark Python API (PySpark)](https://spark.apache.org/docs/latest/api/python/)
- [ElasticSearch Guide](https://www.elastic.co/guide/en/elasticsearch/reference/7.15/index.html)
- [Kibana Guide](https://www.elastic.co/guide/en/kibana/7.15/index.html)

### Docker Images

- [Big Data Europe Hadoop](https://github.com/big-data-europe/docker-hadoop)
- [Big Data Europe Spark](https://github.com/big-data-europe/docker-spark)
- [Official ElasticSearch](https://hub.docker.com/_/elasticsearch)

### Tutorials & Books

- **"Hadoop: The Definitive Guide"** - Tom White
- **"Learning Spark"** - Holden Karau et al.
- **"Elasticsearch: The Definitive Guide"** - Clinton Gormley

### Online Resources

- [Hadoop Tutorial](https://hadoop.apache.org/docs/stable/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html)
- [Spark Programming Guide](https://spark.apache.org/docs/latest/rdd-programming-guide.html)
- [PySpark Examples](https://github.com/apache/spark/tree/master/examples/src/main/python)

---

## 🤝 Contributing

Nếu bạn tìm thấy bugs hoặc muốn cải thiện project:

1. Fork repository
2. Tạo feature branch
3. Commit changes
4. Push và tạo Pull Request

---

## 📝 License

This project is for educational purposes only.

---

## 👨‍💻 Credits & Contact

**Dự án thực hành môn**: Hệ Thống Phân Tán và Xử Lý Dữ Liệu Lớn

**Technologies**:
- Apache Hadoop & YARN
- Apache Spark
- ElasticSearch & Kibana
- Docker & Docker Compose

**Created**: 2025

---

## 🎓 Learning Outcomes

Sau khi hoàn thành các labs, bạn sẽ:

✅ Hiểu kiến trúc Hadoop HDFS và distributed storage  
✅ Lập trình MapReduce với Java  
✅ Xử lý dữ liệu nhanh với Apache Spark (PySpark)  
✅ Build real-time streaming applications  
✅ Implement search engine với ElasticSearch  
✅ Monitor và troubleshoot Big Data applications  
✅ Deploy distributed systems với Docker  

---

## 📞 Support

Nếu gặp vấn đề:

1. Kiểm tra [Troubleshooting](#️-troubleshooting) section
2. Xem logs: `docker-compose logs -f <service>`
3. Kiểm tra Web UIs
4. Restart services: `docker-compose restart`

---

**Happy Learning! 🎉**

*Built with ❤️ using Hadoop, Spark, and ElasticSearch*
