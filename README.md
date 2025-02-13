# Data Engineering Project

This repository contains the code and documentation for a Data Engineering project that collects, transforms, and analyzes daily taxi trip data from Chicago and corresponding historical weather data. The project leverages AWS services to create an efficient data pipeline and perform analytical queries.

## Project Overview
The primary objective of this project is to:

1. Collect taxi trip data from the City of Chicago's open data portal.
2. Combine the taxi data with historical weather data to explore correlations.
3. Transform and store the raw data in CSV format for further analysis.
4. Analyze the data using AWS Athena.

## Data Sources
- **Taxi Trip Data**: [City of Chicago Open Data Portal](https://data.cityofchicago.org/resource/ajtu-isnz.json?)
- **Historical Weather Data**: [Open-Meteo Archive API](https://archive-api.open-meteo.com/v1/era5)

## Technology Stack
This project uses the following technologies:

- **AWS S3**: To store raw and processed data files.
- **AWS Lambda**: To automate the transformation of raw JSON data into CSV format.
- **AWS Athena**: To perform SQL queries and analyze the combined datasets.
- **Python**: For data collection and preprocessing scripts.

## Architecture
1. **Data Collection**: Daily taxi trip data is retrieved from the City of Chicago Open Data portal, and historical weather data is fetched from the Open-Meteo Archive API.
2. **Data Storage**: Raw JSON files are stored in an Amazon S3 bucket.
3. **Data Transformation**: AWS Lambda functions process the raw JSON files into CSV format and upload the transformed files to a separate S3 bucket.
4. **Data Analysis**: The processed data is queried using AWS Athena, enabling detailed analysis and insights.

## Setup Instructions

### Prerequisites
- AWS account with S3, Lambda, and Athena services enabled.
- Python 3.8 or higher installed locally.

### Steps
1. **Clone the repository:**
   ```bash
   git clone https://github.com/rhamorszky/data_engineering_project.git
   cd data_engineering_project
   ```

2. **Install dependencies:**
   Use a virtual environment to install Python dependencies.
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. **Configure AWS Credentials:**
   Set up your AWS credentials using the AWS CLI or environment variables.
   ```bash
   aws configure
   ```

4. **Deploy AWS Lambda Function:**
   - Package your Lambda function code into a ZIP file.
   - Deploy the function using the AWS Management Console or CLI.

5. **Set Up S3 Buckets:**
   - Create two S3 buckets: one for raw data and another for transformed data.
   - Update the S3 bucket names in the Lambda function configuration.

6. **Run Data Pipeline:**
   - Schedule the Lambda function to run daily using AWS CloudWatch.

7. **Analyze Data with AWS Athena:**
   - Configure an Athena table to query the processed CSV files.
   - Use SQL queries to perform analysis.

## Example Queries
Here are some example Athena queries:

1. **Top 10 Days with Highest Taxi Rides:**
   ```sql
   SELECT ride_date, COUNT(*) AS ride_count
   FROM taxi_weather_data
   GROUP BY ride_date
   ORDER BY ride_count DESC
   LIMIT 10;
   ```

2. **Impact of Weather on Taxi Rides:**
   ```sql
   SELECT weather_condition, AVG(ride_count) AS avg_rides
   FROM taxi_weather_data
   GROUP BY weather_condition
   ORDER BY avg_rides DESC;
   ```


## Visualizations
![Correlation Matrix Heatmap for hourly ride count](Fig1_correlation_matrix_heatmap_hourly_ride_count.png)
![Hourly Ride Count by Hour of the Day](Fig2_hourly_ride_count_by_hour.png)
![Ride Count by Hour and Day of Week](Fig3_ride_count_by_hour_and_day_of_week.png)
![Average Fare by Day of the Week](Fig4_average_fare_by_day.png)
![Correlation Matrix Heatmap for hourly average fare](Fig5_correlation_matrix_heatmap_hourly_avg_fare.png)
![Average Fare by Day and Hour](Fig6_average_fare_by_day_hour.png)
![Avg Fare by Hour and Day of Week](Fig7_avg_fare_by_hour_and_day_of_week.png)



## Future Enhancements
- Add visualization tools (e.g., Tableau, Power BI) for better insights.
- Expand the data pipeline to include additional data sources.


## Contact
For any questions or feedback, feel free to contact the repository owner.