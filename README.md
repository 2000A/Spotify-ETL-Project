# Spotify-ETL-Project
This Project is part of my python course for data engineering by DataVidhya platform. Its an End-to-End ETL pipeline project that fetches the spotify playlist details using spotify api and does tranformation and analysis using AWS cloud
# 🎧 Spotify End-to-End Data Pipeline Project

This project is part of the **Python for Data Engineering** course by **DataVidya**.

## 🧠 Business Problem

A client with a strong passion for the music industry wants to understand current trends by analyzing top-performing global songs on Spotify. The goal is to collect this data consistently over a year to identify patterns and insights that can guide future music production.

To do this, we’ve built a fully automated data pipeline using AWS services and the Spotify API. The pipeline collects daily data from Spotify's Top 50 Global Songs playlist and stores, transforms, and makes it available for querying and analysis.

---

## 🚀 Project Overview

- **Data Source**: [Spotify Top 50 – Global](https://open.spotify.com/playlist/37i9dQZEVXbMDoHDwVN2tF)
- **Pipeline Components**: Spotify API, AWS Lambda, Amazon S3, AWS CloudWatch, AWS Glue, Amazon Athena
- **Goal**: Collect and analyze daily top songs globally on Spotify to discover trends in the music industry

---

## 🧩 Architecture
Spotify API --> AWS Lambda (Extract) --> S3 (Raw Data)
↑
CloudWatch (Daily Trigger)

S3 (Raw Data) --> AWS Lambda (Transform) --> S3 (Transformed Data)
↑
S3 Trigger

S3 (Transformed Data) --> AWS Glue Crawler --> Glue Catalog --> Amazon Athena (SQL Queries)


---

## 📦 Extract

### Technologies Used:
- `spotipy` Python package
- **AWS Lambda**
- **Amazon CloudWatch**
- **Amazon S3**

### Process:
1. Register on [Spotify for Developers](https://developer.spotify.com/) to get `Client ID` and `Client Secret`.
2. Use `spotipy` to extract the Top 50 Global playlist.
3. Deploy this extract script to AWS Lambda.
4. Trigger this Lambda daily using CloudWatch.
5. Store the raw data in Amazon S3 under:
     S3 Bucket: spotify-etl-project-abhi0009
└── raw_data/
├── to_be_processed/
└── processed/


---

## 🧪 Transform

### Technologies Used:
- **AWS Lambda**
- **Amazon S3 (S3 Triggers)**

### Process:
1. Lambda function processes new files added to `raw_data/to_be_processed/`.
2. Applies transformation:
- Extracts `album_list` and `artist_list`.
- Performs datetime formatting and cleanup.
3. Saves the transformed data to:
transformed_data/
├── album_list/
└── artist_list/
4. Moves the original raw file to `processed/` after transformation.

---

## 🗄️ Load

### Technologies Used:
- **AWS Glue Crawler**
- **Amazon Athena**

### Process:
1. AWS Glue Crawler reads files in `transformed_data/`.
2. Creates a Glue Catalog with schema (columns, data types, etc.).
3. Amazon Athena can now query the catalog using standard SQL.

---

## 🔍 Analysis Goals

Once data is collected over time, the client can:
- Discover top trending genres, artists, and albums.
- Analyze music trends by day, week, or season.
- Understand attributes of top-performing songs (duration, release year, etc.).
- Make data-driven decisions for music creation.

---

## 🛠️ Tools & Services

| Service         | Purpose                          |
|----------------|----------------------------------|
| Spotify API     | Extract top global songs         |
| AWS Lambda      | Serverless data processing       |
| Amazon CloudWatch | Triggers Lambda daily         |
| Amazon S3       | Stores raw and transformed data  |
| AWS Glue        | Creates data catalog             |
| Amazon Athena   | SQL queries on transformed data  |



## 📁 Repository Structure


