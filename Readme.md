Here's the complete `README.md` file content with all the provided details:  


# Amazon Books Data Pipeline

## Project Overview

This project builds an automated data pipeline that collects and processes books data from the Amazon website. The data is scraped using Python, cleaned and transformed, and the entire workflow is automated and managed with Apache Airflow. Docker Compose is used to containerize the entire setup for simplicity and portability. Finally, the processed data is stored in a PostgreSQL database for analysis.

---

## Technologies Used

- Python: For web scraping and data cleaning.
- Apache Airflow: For orchestrating the ETL workflow.
- Docker Compose: To containerize the application.
- PostgreSQL: To store the processed data.

---

## Setup Instructions

### 1. Clone the Repository

Clone the project repository and navigate to the directory:

```bash
git clone https://github.com/your-username/amazon-books-data-pipeline.git
cd amazon-books-data-pipeline
```

### 2. Install Dependencies

Install Python dependencies required for the project:

```bash
pip install -r requirements.txt
```

If you don't have Docker Compose installed, install it using the following command (for Ubuntu):

```bash
sudo apt-get install docker-compose
```

### 3. Configure PostgreSQL

Set up PostgreSQL with the following details:

- **Database Name**: `amazon_books_db`
- **Username**: `your_username`
- **Password**: `your_password`

Update the connection settings in the `config.py` file.

### 4. Docker Setup

Use Docker Compose to set up all necessary services:

- **PostgreSQL**: For storing the processed data.
- **Apache Airflow**: For managing and scheduling the data pipeline.

Start the services by running:

```bash
docker-compose up
```

This will initialize both PostgreSQL and Airflow, running in the background.

### 5. Airflow DAGs Configuration

The pipeline logic is defined in the `scrape_books.py` file inside the `dags/` directory. This file contains the workflow to automate scraping, cleaning, and database insertion tasks.

---

## Running the Pipeline

### 6.1. Accessing the Airflow Web UI

Once the services are running, access the Airflow Web UI at `http://localhost:8080`.

- **Default credentials**:  
  - **Username**: `airflow`  
  - **Password**: `airflow`

### 6.2. Activating the DAG

1. In the Airflow Web UI, navigate to the **DAGs** tab.
2. Locate the DAG named `scrape_books.py`.
3. Toggle the switch to **On** to activate the DAG.

This will execute the following steps:
1. Scrape books data from Amazon using Python.
2. Clean and transform the scraped data.
3. Load the processed data into PostgreSQL for analysis.

### 6.3. Setting Up PostgreSQL Connection in Airflow

To allow Airflow to communicate with PostgreSQL:

1. In the Airflow Web UI, go to **Admin > Connections**.
2. Click the **+** button to create a new connection.
3. Fill in the connection details:
   - **Conn ID**: `postgres_conn` (or any custom name)
   - **Conn Type**: `Postgres`
   - **Host**: `postgres` (default service name in Docker Compose)
   - **Schema**: `amazon_books_db` (or your PostgreSQL database name)
   - **Login**: `your_username`
   - **Password**: `your_password`
   - **Port**: `5432`
4. Save the connection.

### 6.4. Accessing the PostgreSQL Database

#### Using pgAdmin:

1. Open **pgAdmin** and connect to the PostgreSQL server using the credentials set in Airflow.
2. Navigate to the database `amazon_books_db`.
3. Run SQL queries in pgAdmin to analyze the data. Example:

```sql
SELECT * FROM books;
```

#### Using the Terminal (`psql`):

1. Connect to the database using the following command:

```bash
psql -h localhost -U your_username -d amazon_books_db
```

2. Run queries to explore the data, such as:

```sql
SELECT * FROM books;
```

### 6.5. Analyzing the Data

Perform analysis on the data using SQL queries. Example:

```sql
SELECT category, COUNT(*) AS book_count 
FROM books 
GROUP BY category
ORDER BY book_count DESC;
```

This query provides a count of books per category, sorted by the highest count.

---



## Future Improvements

- Implement error handling for scraping failures.
- Schedule regular scraping to keep data updated.
- Explore advanced transformation techniques for data cleaning.
- Deploy the pipeline on cloud platforms like AWS or Azure for scalability.

---
