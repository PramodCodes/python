# 67 - 72 Python 13 Feb-2024

---

## Python 1

### Need of python ? &difference between python and shell script

Shell scripting is used for

- System Administration
  - Automating route system administration tasks
  - Starting and stopping services
  - Managing users
  - Basic file manipulation
- Command line interactions
- Rapid Prototyping
- Text Processing
  - Text manipulation e.g. parsing logs, searching and replacing text, extracting data from text-based resources
- Environment Variables and configuration

---

### **Use Cases and Scenarios for Shell Scripting**

Shell scripting is a powerful tool for automating repetitive tasks, system administration, text processing, and more. Below are detailed **use cases** and **real-world scenarios** where shell scripting is highly beneficial.

---

## **1. System Administration**

### **Use Cases:**

✅ Automating routine administrative tasks
✅ Managing services
✅ Scheduling backups
✅ System monitoring

### **Scenarios:**

- **Automated Service Restart**: Restart a service automatically if it crashes.
  ```bash
  # Restart nginx if not running
  if ! systemctl is-active --quiet nginx; then
      systemctl restart nginx
  fi
  ```
- **User Management**: Create multiple users in bulk.
  ```bash
  for user in user1 user2 user3; do
      useradd $user
      echo "Password123" | passwd --stdin $user
  done
  ```
- **Automated Backup**: Schedule backups using cron jobs.
  ```bash
  tar -czf /backup/home_backup_$(date +%F).tar.gz /home
  ```

---

## **2. Command Line Interactions**

### **Use Cases:**

✅ Automating complex CLI commands
✅ Running multiple commands in sequence
✅ Interactive scripts for user input

### **Scenarios:**

- **Batch File Renaming**: Rename all `.txt` files to `.log`.
  ```bash
  for file in *.txt; do
      mv "$file" "${file%.txt}.log"
  done
  ```
- **Automated Log Cleanup**: Delete logs older than 30 days.
  ```bash
  find /var/log -type f -mtime +30 -delete
  ```
- **Interactive Script for User Input**:
  ```bash
  read -p "Enter your name: " name
  echo "Hello, $name!"
  ```

---

## **3. Rapid Prototyping**

### **Use Cases:**

✅ Quickly testing new ideas before full implementation
✅ Generating temporary configurations
✅ Automating simple program execution

### **Scenarios:**

- **Mock API Response Testing**:
  ```bash
  echo '{"status": "success", "message": "API is working"}' | jq .
  ```
- **Network Connectivity Test**:
  ```bash
  for ip in 8.8.8.8 1.1.1.1; do
      ping -c 2 $ip
  done
  ```
- **Quick Web Scraper**:
  ```bash
  curl -s https://example.com | grep "title"
  ```

---

## **4. Text Processing**

### **Use Cases:**

✅ Log file analysis
✅ Searching and extracting data
✅ Automating report generation

### **Scenarios:**

- **Extract Failed Login Attempts from Logs**:
  ```bash
  grep "Failed password" /var/log/auth.log
  ```
- **Find and Replace Text in Files**:
  ```bash
  sed -i 's/oldtext/newtext/g' file.txt
  ```
- **Word Frequency Analysis**:
  ```bash
  cat file.txt | tr -s ' ' '\n' | sort | uniq -c | sort -nr
  ```

---

## **5. Environment Variables and Configuration**

### **Use Cases:**

✅ Setting up environment variables
✅ Managing system-wide settings
✅ Automating software installations

### **Scenarios:**

- **Exporting Environment Variables**:
  ```bash
  export PATH=$PATH:/custom/path
  ```
- **Dynamic Configuration File Generation**:
  ```bash
  echo "server_name=example.com" > config.ini
  ```
- **Automating Software Installation**:
  ```bash
  sudo apt update && sudo apt install -y nginx
  ```

---

### **Conclusion**

| **Category**                  | **Scenarios**                                    |
| ----------------------------------- | ------------------------------------------------------ |
| **System Administration**     | Service restart, User management, Backups              |
| **Command Line Interactions** | File renaming, Log cleanup, Interactive scripts        |
| **Rapid Prototyping**         | Mock API testing, Connectivity test, Web scraping      |
| **Text Processing**           | Log analysis, Text replacement, Word frequency         |
| **Environment & Configs**     | Setting ENV variables, Config files, Software installs |

Shell scripting is invaluable in **automating tasks**, **improving efficiency**, and **managing systems**. Let me know if you need more examples! 🚀

---



## Python

Multip purpose programming language , Image processing , deep learning etc

As a DevOps engineer 

* To write Complex logic: data structures, algorithms, data manipulation

- Cross platform compatiability: Windows, Linux, Unix, Mac (shell script only works in Linux, to make our scripts compatable we will make this python)
- API Integration: Application Programming Interface (API)
  - API is Request and Response system
- Reusable code (DRY)
- Error Handling: try, except and finally block
- Advanced Data Processing


### **Python Usage in DevOps**

As a DevOps engineer, Python plays a critical role in automating, managing, and optimizing infrastructure and CI/CD pipelines. Below are the key **use cases** and **scenarios** where Python is used effectively in DevOps.

---

## **1. Writing Complex Logic (DS, Algorithms, Data Manipulation)**

✅ Python provides rich support for  **data structures** ,  **algorithms** , and **file manipulation** to process log files, manage configurations, and automate tasks.

### **Scenarios**

* **Processing Large Log Files Efficiently**
  ```python
  with open("/var/log/syslog") as f:
      error_logs = [line for line in f if "ERROR" in line]
  print(error_logs)
  ```
* **Sorting and Filtering Data**
  ```python
  server_loads = {"server1": 80, "server2": 55, "server3": 92}
  sorted_servers = sorted(server_loads.items(), key=lambda x: x[1])
  print(sorted_servers)  # Sorted by CPU load
  ```
* **Parsing JSON/YAML Configurations**
  ```python
  import json
  config = json.load(open("config.json"))
  print(config["database"]["host"])
  ```

---

## **2. Cross-Platform Compatibility**

✅ Unlike shell scripts, which work only on Linux, Python is **cross-platform** and runs on Windows, macOS, Linux, and Unix.

### **Scenarios**

* **Platform-Specific Task Execution**
  ```python
  import os
  if os.name == "nt":
      print("Running on Windows")
  else:
      print("Running on Linux/Mac")
  ```
* **File Operations Across Platforms**
  ```python
  import shutil
  shutil.copy("source.txt", "destination.txt")  # Works on all OS
  ```

---

## **3. API Integration (REST API & Webhooks)**

✅ DevOps engineers frequently interact with APIs (Kubernetes, AWS, Jenkins, Terraform, etc.). Python’s `requests` module makes API calls simple.

### **Scenarios**

* **Get Server Status via API**
  ```python
  import requests
  response = requests.get("https://api.server.com/status")
  print(response.json())
  ```
* **Trigger Jenkins Job via API**
  ```python
  import requests
  jenkins_url = "http://jenkins.example.com/job/deploy/build"
  requests.post(jenkins_url, auth=("user", "password"))
  ```
* **Automate Cloud Provisioning with Terraform API**
  ```python
  terraform_apply = requests.post("http://terraform.example.com/apply")
  print(terraform_apply.status_code)
  ```

---

## **4. Reusable Code (DRY - Don't Repeat Yourself)**

✅ DevOps engineers aim to avoid redundant scripts by creating reusable Python modules.

### **Scenarios**

* **Reusable SSH Connection Function**
  ```python
  import paramiko

  def connect_ssh(host, user, password):
      ssh = paramiko.SSHClient()
      ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
      ssh.connect(host, username=user, password=password)
      return ssh

  ssh_client = connect_ssh("192.168.1.100", "admin", "password123")
  stdin, stdout, stderr = ssh_client.exec_command("ls -l")
  print(stdout.read().decode())
  ssh_client.close()
  ```
* **Reusable AWS S3 Upload Function**
  ```python
  import boto3

  def upload_to_s3(bucket, file_path):
      s3 = boto3.client("s3")
      s3.upload_file(file_path, bucket, file_path.split("/")[-1])

  upload_to_s3("my-bucket", "/path/to/file.txt")
  ```

---

## **5. Error Handling (try, except, finally)**

✅ Robust error handling prevents scripts from failing unexpectedly.

### **Scenarios**

* **Handling API Request Failures**
  ```python
  try:
      response = requests.get("https://api.server.com")
      response.raise_for_status()
  except requests.exceptions.RequestException as e:
      print(f"API request failed: {e}")
  finally:
      print("Execution completed.")
  ```
* **Handling File Operations Safely**
  ```python
  try:
      with open("config.yaml", "r") as file:
          config = file.read()
  except FileNotFoundError:
      print("File not found!")
  ```

---

## **6. Advanced Data Processing**

✅ DevOps engineers often work with logs, monitoring data, and metrics, requiring advanced data processing.

### **Scenarios**

* **Analyzing CPU Usage from Logs**
  ```python
  import re

  with open("/var/log/syslog") as f:
      cpu_usage = [line for line in f if re.search(r"CPU Usage: \d+%", line)]
  print(cpu_usage)
  ```
* **Extracting Key Metrics from Kubernetes Logs**
  ```python
  import json

  logs = '[{"pod": "web-1", "cpu": 80}, {"pod": "db-1", "cpu": 95}]'
  log_data = json.loads(logs)

  for log in log_data:
      if log["cpu"] > 90:
          print(f"High CPU Usage Detected in {log['pod']}")
  ```

---

## **Conclusion: Why Python for DevOps?**

| **Feature**                            | **Shell Script**  | **Python**               |
| -------------------------------------------- | ----------------------- | ------------------------------ |
| **Cross-Platform Compatibility**       | ❌ No (Linux only)      | ✅ Yes (Windows, Linux, Mac)   |
| **Complex Logic (DS, Algorithms)**     | ❌ Hard to implement    | ✅ Built-in libraries          |
| **API Integration (REST, Webhooks)**   | ❌ Limited              | ✅ Powerful `requests`module |
| **Error Handling**                     | ❌ Limited (`set -e`) | ✅`try-except-finally`       |
| **Reusable Code (Functions, Modules)** | ❌ No                   | ✅ Yes (`import`)            |
| **Advanced Data Processing**           | ❌ Basic                | ✅ Regex, JSON, YAML, Pandas   |

### **Final Thoughts**

Python is **indispensable in DevOps** because of its  **flexibility, automation capabilities, and cross-platform support** . From  **API interactions** ,  **error handling** , and **log processing** to  **CI/CD automation** ,  **configuration management** , and  **cloud orchestration** , Python simplifies and streamlines DevOps workflows.

Let me know if you need more details! 🚀

---



### **Why Was Python 3 Created When Python 2 Already Existed?**

Python 3 was introduced to **fix fundamental design flaws** in Python 2 that hindered long-term development, security, and maintainability. Python 2 had several limitations, and instead of continuing to patch an outdated architecture, the Python community decided to create Python 3 as a  **modern, forward-compatible language** .

---

## **Key Reasons for Creating Python 3**

### **1. Unicode Support by Default (Better Internationalization)**

#### 🔴 Problem in Python 2:

* Strings were ASCII by default, leading to encoding issues when working with non-English characters.
* Developers had to explicitly use Unicode (`u"string"`) or handle encoding errors manually.

#### ✅ Solution in Python 3:

* **All strings (`str`) are Unicode by default** , making text handling easier.
* **No need to manually handle encoding/decoding** .

**Example: Handling Unicode Characters**
Python 2:

```python
print u"Hello, 你好"  # Unicode needs explicit 'u' prefix
```

Python 3:

```python
print("Hello, 你好")  # No need for 'u', Unicode by default
```

---

### **2. Print Statement Changed to Print Function**

#### 🔴 Problem in Python 2:

* `print` was a  **statement** , not a function, making it inconsistent with other built-in functions.
* Print syntax differed from function calls.

#### ✅ Solution in Python 3:

* `print()` is now a  **function** , making it consistent and allowing advanced formatting.

**Example:**
Python 2:

```python
print "Hello, World"  # No parentheses
```

Python 3:

```python
print("Hello, World")  # Uses parentheses
```

---

### **3. Better Integer Division (Avoids Common Bugs)**

#### 🔴 Problem in Python 2:

* Division of two integers would return an  **integer** , potentially leading to incorrect results.

#### ✅ Solution in Python 3:

* **Division now returns a float** , making calculations more intuitive.
* If integer division is needed, `//` must be explicitly used.

**Example:**
Python 2:

```python
print 5 / 2  # Output: 2 (incorrect for most use cases)
```

Python 3:

```python
print(5 / 2)  # Output: 2.5 (correct behavior)
print(5 // 2)  # Output: 2 (integer division)
```

---

### **4. Improved Iterators and Generators (Better Performance)**

#### 🔴 Problem in Python 2:

* Functions like `range()`, `zip()`, and `map()` returned  **lists** , leading to high memory usage.

#### ✅ Solution in Python 3:

* These functions now return  **iterators** , improving efficiency and performance.

**Example:**
Python 2:

```python
print range(1, 1000000)  # Creates a huge list, consuming memory
```

Python 3:

```python
print(range(1, 1000000))  # Returns an iterator, saving memory
```

---

### **5. Improved Exception Handling**

#### 🔴 Problem in Python 2:

* The old-style exception syntax (`except Exception, e:`) was inconsistent and error-prone.

#### ✅ Solution in Python 3:

* Exception syntax is more structured and Pythonic.

**Example:**
Python 2:

```python
try:
    x = 1 / 0
except ZeroDivisionError, e:  # Old syntax
    print "Error:", e
```

Python 3:

```python
try:
    x = 1 / 0
except ZeroDivisionError as e:  # New syntax
    print("Error:", e)
```

---

### **6. Removal of Deprecated and Confusing Features**

#### 🔴 Problem in Python 2:

* Several outdated features existed for backward compatibility, leading to confusion.

#### ✅ Solution in Python 3:

* Removed redundant functions like `xrange()` (replaced by `range()`) and old-style classes.

**Example:**
Python 2:

```python
print type(5) == int  # Output: False (confusing behavior)
```

Python 3:

```python
print(type(5) == int)  # Output: True (consistent behavior)
```

---

### **7. More Consistent and Clean Codebase**

Python 3 eliminated many design inconsistencies, making it easier to learn and maintain.

✅ **Example Improvements**

* `input()` replaces `raw_input()`.
* `keys()`, `values()`, and `items()` return **iterators** instead of lists.
* `super()` no longer requires explicit arguments (`super(Class, self)` → `super()`).

---

## **Why Not Just Fix Python 2 Instead of Making Python 3?**

1. **Backward compatibility issues** : Many fundamental problems in Python 2 couldn’t be fixed without breaking compatibility.
2. **Technical debt** : Python 2 had too many legacy issues, making future development harder.
3. **Cleaner and modern design** : Python 3 was an opportunity to build a more **consistent, efficient, and Pythonic** language.

---

## **Python 2 End of Life (EOL)**

* Python 2 was officially  **deprecated on January 1, 2020** .
* No security patches or updates are provided.
* Developers should  **migrate to Python 3** .

---

## **Final Comparison: Python 2 vs Python 3**

| Feature                      | Python 2              | Python 3                              |
| ---------------------------- | --------------------- | ------------------------------------- |
| **Unicode Strings**    | ❌ No (ASCII default) | ✅ Yes (Unicode default)              |
| **Print Statement**    | `print "text"`      | `print("text")`                     |
| **Integer Division**   | ❌`5 / 2 = 2`       | ✅`5 / 2 = 2.5`                     |
| **Range() Function**   | Returns list          | Returns iterator                      |
| **Exception Handling** | `except Error, e:`  | `except Error as e:`                |
| **Memory Efficiency**  | ❌ Less efficient     | ✅ More efficient                     |
| **Active Support**     | ❌ No (EOL 2020)      | ✅ Yes (Current version: Python 3.12) |

---

### **Conclusion**

Python 3 was created because **Python 2 had fundamental design flaws** that couldn’t be fixed without breaking existing code. Python 3 provides  **better performance, security, and consistency** , making it the  **standard for all modern Python development** .

**🚀 If you're starting a new project, always use Python 3!**

---





### Basics of python 


---

- There are 2 major versions in Python i.e. Python v2 and Python v3
- Python v2 has reached its EOL (End of life) 20 April 2020
- Python v3 initial release was on 3 December 2008
- Scripts in python are saved using .py extension
- To run a python script, we use: python hello_world.py
- Python is case-sensitive which means python treats A and a as different
- To comment a line of code in python, we use: # -> Single line comment
- Similarly, you can also comment out a block of code using:
  """
  """
- Also, you can write an inline comment along with the line of code
  e.g. print("Hello World") # This line of code prints Hello World

Variables 48:00
---------------

- It is a box to store some data inside it and use it when ever needed

Data types:
-----------

- Numeric datatypes:

  - int: e.g. 1, 2, 20, 40 etc
  - float: e.g. 1.22, 2.34, 4.35
  - complex: e.g. 1 + 2j, 4 + 5j
- Boolean type: True, False
- Sequence types:

  - str: 'a', "Hello world",
    """
    This is a
    multiline string
    """
  - list:
  - tuple:
- Mapping type: dict
- Set types: set, frozenset (immutable)
- Binary type: byte (immutable sequences of bytes), bytearray (mutable sequences of bytes)
- None Type
- Custom datatypes

  - This is usually defined using Classes
- To identify the datatype of a variable, we can use a function called as: type()
- It is important to know the datatype, as there are specific methods that can be applied to those datatypes
