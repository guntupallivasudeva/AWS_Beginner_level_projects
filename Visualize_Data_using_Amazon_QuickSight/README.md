
# 🧠 Beginner AWS QuickSight Project with Amazon S3

Welcome to my beginner-level AWS QuickSight project! This project focuses on building interactive dashboards by connecting Amazon QuickSight with data stored in Amazon S3. It's designed to showcase how cloud-native tools can be used for data analysis and visualization.

## 🚀 Project Objective

To analyze and visualize customer sales data stored in an Amazon S3 bucket using Amazon QuickSight, with the help of AWS Quick Sight

---

## 🛠️ Tools & Services Used

- **Amazon S3** – to store CSV data
- **Amazon QuickSight** – for dashboard creation and visualization
- **IAM** – to set up appropriate access permissions

---

## 📁 Project Structure

```
aws-quicksight-s3-dashboard/
│
├── sample-data/
│   └── Amazon-Bestseller-Data.csv          # Sample CSV uploaded to S3
├── screenshots/
│   └── dashboard-preview.png       # Final dashboard view (optional)
├── README.md                       # Project documentation (this file)
```

---

## 📊 Dataset Description

The dataset is a simple CSV file containing mock customer sales data with the following columns:

| CustomerID | Region | Product | Sales | Date       |
|------------|--------|---------|-------|------------|
| 001        | North  | A       | 120   | 2024-01-01 |
| 002        | East   | B       | 150   | 2024-01-02 |
| ...        | ...    | ...     | ...   | ...        |

---
# First Method

## 🧩 Step-by-Step Process

### 1. 📥 Upload Data to S3
- Go to the AWS Management Console → S3
- Create a new bucket (e.g., `quicksight-data-project`)
- Upload `Amazon-Bestseller-Data.csv` into a folder 
- upload manifest.json file which provide in github


### 2. 🛡️ Set Up Permissions
- Create or use an IAM role with the following permissions:
  - `AmazonS3ReadOnlyAccess`
  - `AWSGlueConsoleFullAccess`
  - `AmazonQuickSightFullAccess`

- Ensure that QuickSight is allowed to access S3 and Glue via **Manage QuickSight > Security & permissions**

### 4. 📈 Create Dashboard in QuickSight
- Go to **Amazon QuickSight**
- Choose **New Analysis** > **New Dataset** > Choose **AWS S3 Bucket Url**
- Build visualizations:
  - **Bar charts** for Sales by Region
  - **KPI** card for Total Sales
  - **Line chart** for Sales Over Time
  - **Filters** for Date or Product

### 5. 💾 Save and Share
- Save your analysis
- Create a dashboard from it
- (Optional) Share it with your AWS account users or embed it securely in applications

# Second Method

## 🏷️ Tags

`AWS` `QuickSight` `S3` `Data Visualization` `Beginner Project` `Cloud Computing` `Dashboard`

In this project, you'll learn how to create visualizations from a large dataset using Amazon S3 and Amazon Quicksight. We'll be working with a dataset of 50,000 best-selling products on Amazon.com.

### Step #1: Download the Dataset
- Navigate to [AWS_Beginner_level_projects/Visualize_Data_using_Amazon_QuickSight](https://github.com/guntupallivasudeva) to download the "Amazon Bestseller Dataset" CSV file and the "manifest.json" file.
- Click on "raw" and Control+S to save both files onto your computer.

### Step #2: Store the Dataset in Amazon S3
- Open the Amazon S3 console and click "Create Bucket."
- Name the bucket (e.g., "beginner-quick-sight-project") and keep the settings as default.
- Upload the CSV file and the "manifest.json" file into the bucket.
- Replace the URL in the "manifest.json" file with the S3 URL of your dataset.

### Step #3: Connect S3 Bucket with Amazon Quicksight
- Open the AWS management console and navigate to Amazon Quicksight.
- Sign up for a free trial of the Enterprise edition if you don't have an account.
- Select Amazon S3 and tick the box for the S3 bucket you created.
- Enter the link to your "manifest.json" file and connect to Quicksight.
- Select "interactive sheet" to start creating visualizations.

### Step #4: Create Visualizations
- Drag fields into the graph to create visualizations (e.g., Most popular brands).
- Sort, filter, and customize the graphs as desired.
- Experiment with different types of graphs like bar charts, pie charts, line graphs, etc.
---

## 🎓 Key Learnings

- Connected AWS S3 with QuickSight using AWS Glue
- Understood how to catalog semi-structured data
- Built dashboards with various charts and filters
- Applied IAM policies for controlled access

---

## 📸 Dashboard Preview

[Quick-Sight Dashboard ](6.png)

---

## 📌 Future Enhancements

- Integrate more complex datasets (e.g., from RDS or Redshift)
- Automate Glue crawlers using Lambda
- Use calculated fields in QuickSight for deeper insights

---

## 📬 Contact

**Guntupalli Vasudeva**  
[LinkedIn](https://www.linkedin.com/in/gvasudeva) | [GitHub](https://github.com/guntupallivasudeva)  

----
