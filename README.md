Data Processing Script (scripts/data_processing.py)
--------------------------------------------------
from pyspark.sql import SparkSession

def process_data(input_path, output_path):
    spark = SparkSession.builder.appName("Data Processing").getOrCreate()
    df = spark.read.parquet(input_path)
    df = df.withColumn("value", df["value"] * 1.1)
    df.write.parquet(output_path)
    spark.stop()

if __name__ == "__main__":
    input_path = "data/processed/sample_data.parquet"
    output_path = "data/processed/processed_data.parquet"
    process_data(input_path, output_path)
