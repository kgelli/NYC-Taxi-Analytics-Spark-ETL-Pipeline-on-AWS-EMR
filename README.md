# AWS EMR Data Processing for Data Engineers

## Project Summary

This project demonstrates the use of Amazon Elastic Map Reduce (EMR) for processing large datasets using Apache Spark. It includes a Spark script for ETL (Extract, Transform, Load) operations, AWS command line instructions for setting up and managing the EMR cluster, and a dataset for testing and demonstration purposes.

## Architecture

![AWS EMR Architecture](architecture.png)

- **S3**: Source and destination storage
- **EMR**: Managed Spark cluster
  - Master node coordinates jobs
  - Worker nodes execute processing in parallel
- **PySpark**: Processing framework for transformation logic

## Files

- `spark-etl.py`: Reads data from an input directory, adds a timestamp, and writes the result to an output directory in Parquet format
- `commands.py`: Contains scripts for AWS EMR cluster setup and management
- `tripdata.csv`: Sample NYC taxi data (20,000 records) for testing and demonstration

## Usage

1. **Upload to S3**
   ```bash
   aws s3 cp spark-etl.py s3://<YOUR-BUCKET>/files/
   aws s3 cp tripdata.csv s3://<YOUR-BUCKET>/input/
   ```

2. **Run on EMR**
   ```bash
   ssh -i <key-pair.pem> hadoop@<emr-master-dns>
   spark-submit spark-etl.py s3://<YOUR-BUCKET>/input s3://<YOUR-BUCKET>/output
   ```

## Output

- Transformed data in Parquet format
- Added timestamp column
- Schema and record count information printed

## Requirements

- Apache Spark
- AWS CLI
- An AWS account with necessary permissions to create and manage EMR clusters

## Conclusion

This ETL pipeline demonstrates a serverless approach to big data processing, leveraging AWS managed services to handle scalable workloads. The architecture can be easily extended to accommodate larger datasets, additional transformations, or integration with data warehousing solutions for analytics.
