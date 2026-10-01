<header>

<h1>🚕 NYC Taxi Azure Data Engineering</h1>

<p>
Building an automated end-to-end cloud data engineering pipeline using
Azure Data Factory, Azure Data Lake Storage Gen2, Azure Databricks,
PySpark and Delta Lake.
</p>

</header>

---

## 📌 Table of Contents

- ## 📌 Table of Contents

- <a href="#overview">📌 Project Overview</a>
- <a href="#business-problem">💼 Business Problem</a>
- <a href="#dataset">📊 Dataset</a>
- <a href="#tools-technologies">🛠 Tools & Technologies</a>
- <a href="#architecture">🏗 Project Architecture</a>
- <a href="#data-ingestion">🔄 Azure Data Factory – Data Ingestion</a>
- <a href="#databricks">⚡ Azure Databricks & PySpark</a>
- <a href="#data-transformation">🔧 Data Transformation</a>
- <a href="#data-quality">✅ Data Quality Checks</a>
- <a href="#challenges">⚠️ Challenges & Solutions</a>
- <a href="#pipeline-workflow">🔁 Pipeline Workflow</a>
- <a href="#learnings">🎓 Key Learnings</a>
- <a href="#future-improvements">🚀 Future Improvements</a>
- <a href="#contact">👩‍💻 Author & Contact</a>

---

<h2>📌 Project Overview</h2>

<p>
This project demonstrates an end-to-end Azure Data Engineering solution
using NYC Taxi trip data.
</p>

<p>
The project automatically extracts monthly NYC Taxi datasets from a web
source using <strong>Azure Data Factory</strong>. The data is stored in
<strong>Azure Data Lake Storage Gen2</strong> and transformed using
<strong>Azure Databricks and PySpark</strong>.
</p>

<p>
The final transformed datasets are stored in a Gold layer where they can
be used for analytics and reporting.
</p>

</section>


<section id="problem">

<h2>💼 Business Problem</h2>

<p>
NYC Taxi generates a large amount of transportation data every month.
Manually downloading and processing each monthly dataset can be
time-consuming and difficult to scale.
</p>

<p>The goal of this project was to:</p>

<ul>

<li>Automate monthly data ingestion</li>

<li>Build a scalable Azure data pipeline</li>

<li>Store large datasets in cloud storage</li>

<li>Clean and transform the data using PySpark</li>

<li>Create analytics-ready datasets</li>

<li>Reduce manual processing</li>

<li>Prepare data for future Power BI reporting</li>

</ul>

</section>



<section id="dataset">

<h2>📊 Dataset</h2>

<p>
The project uses publicly available NYC Taxi trip data provided by the
New York City Taxi & Limousine Commission.
</p>

<a class="btn"
href="https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page"
target="_blank">
View NYC Taxi Dataset
</a>

<h3>Example Fields</h3>

<ul>

<li>VendorID</li>

<li>Pickup Date & Time</li>

<li>Drop-off Date & Time</li>

<li>Passenger Count</li>

<li>Trip Distance</li>

<li>Pickup Location ID</li>

<li>Drop-off Location ID</li>

<li>Payment Type</li>

<li>Fare Amount</li>

<li>Tip Amount</li>

<li>Total Amount</li>

</ul>


<h3>Taxi Zone Dataset</h3>

<ul>

<li>LocationID</li>

<li>Borough</li>

<li>Zone</li>

<li>service_zone</li>

</ul>

</section>

<section id="tools">

<h2>🛠 Tools & Technologies</h2>

<div class="tech">

<div class="card">Azure Data Factory</div>

<div class="card">Azure Data Lake Gen2</div>

<div class="card">Azure Databricks</div>

<div class="card">PySpark</div>

<div class="card">Apache Spark</div>

<div class="card">Delta Lake</div>

<div class="card">Parquet</div>

<div class="card">Unity Catalog</div>

<div class="card">Managed Identity</div>

<div class="card">Azure Access Connector</div>

<div class="card">Python</div>

<div class="card">SQL</div>

<div class="card">Power BI</div>

<div class="card">GitHub</div>

</div>

</section>

<section id="architecture">

<h2>🏗 Project Architecture</h2>

<div class="architecture">

NYC Taxi Website

<br>↓<br>

Azure Data Factory

<br>

Parameters → ForEach → If Condition → Copy Data

<br>↓<br>

Azure Data Lake Storage Gen2

<br>↓<br>

Silver Layer

<br>↓<br>

Azure Databricks

<br>

PySpark Cleaning & Transformation

<br>↓<br>

Gold Layer

<br>↓<br>

Power BI / Analytics

</div>

</section>

<section>

<h2>📁 Project Structure</h2>

<pre>
NYC-Taxi-Azure-Data-Engineering/

│
├── README.md
│
├── architecture/
│   └── architecture-diagram.png
│
├── adf/
│   ├── pipeline-json/
│   └── screenshots/
│
├── databricks/
│   ├── notebooks/
│   ├── transformation.py
│   └── trip_zone.py
│
├── screenshots/
│
├── sql/
│   └── queries.sql
│
├── dashboard/
│   └── nyc_taxi_dashboard.pbix
│
├── presentation/
│   └── NYC_Taxi_Azure_Project.pptx
│
└── dataset/
    └── taxi_zone_lookup.csv
</pre>

</section>

<section id="ingestion">

<h2>🔄 Azure Data Factory – Data Ingestion</h2>

<p>
Azure Data Factory was used to build an automated pipeline for downloading
monthly NYC Taxi datasets.
</p>


<h3>Pipeline Parameters</h3>

<p>
Dynamic parameters were used to generate the NYC Taxi source URLs.
</p>

<pre>
Year = 2026

Month = 01, 02, 03, 04...
</pre>


<h3>ForEach Activity</h3>

<p>
A ForEach activity loops through the required months.
</p>

<pre>
1
2
3
4
5
6
7
</pre>


<h3>If Condition</h3>

<p>
Conditional logic is used to control the pipeline depending on whether
a monthly dataset is available.
</p>


<h3>Copy Data Activity</h3>

<p>
The Copy Data activity transfers the NYC Taxi files from the web source
into Azure Data Lake Storage Gen2.
</p>

</section>



<section id="databricks">

<h2>⚡ Azure Databricks & PySpark</h2>

<p>
Azure Databricks was used for cleaning, transforming and preparing the
NYC Taxi datasets for analytics.
</p>


<h3>Reading Data</h3>

<pre>
df = spark.read.parquet(
    "abfss://silver@nyctaxideepa.dfs.core.windows.net/"
)

display(df)
</pre>


<h3>Removing Duplicates</h3>

<pre>
df = df.dropDuplicates()
</pre>


<h3>Handling Missing Values</h3>

<pre>
df = df.dropna()
</pre>


<h3>Taxi Zone Transformation</h3>

<pre>
from pyspark.sql.functions import col, split

df_trip_type = df_trip_type.withColumn(
    "zone1",
    split(col("Zone"), "/").getItem(0)
)

display(df_trip_type)
</pre>

</section>



<section>

<h2>🥈 Silver Layer</h2>

<p>
The Silver layer contains cleaned and standardized NYC Taxi datasets.
</p>

<ul>

<li>Duplicate removal</li>

<li>Null-value handling</li>

<li>Column transformation</li>

<li>Data-type correction</li>

<li>Invalid record filtering</li>

<li>Taxi zone lookup integration</li>

</ul>

</section>



<section>

<h2>🥇 Gold Layer</h2>

<p>
The Gold layer stores transformed and analytics-ready datasets.
</p>

<pre>
df_gold.write \
.format("delta") \
.mode("overwrite") \
.save(
"abfss://gold@nyctaxideepa.dfs.core.windows.net/trip_zone"
)
</pre>

<p>The Gold layer can support:</p>

<ul>

<li>Trip Analysis</li>

<li>Revenue Analysis</li>

<li>Fare Analysis</li>

<li>Passenger Analysis</li>

<li>Borough Analysis</li>

<li>Taxi Zone Analysis</li>

<li>Power BI Reporting</li>

</ul>

</section>

</section>



<section id="challenges">

<h2>⚠️ Challenges & Solutions</h2>


<h3>1. Monthly Dataset Availability</h3>

<p>
The original pipeline looped through months 1–12. However, the selected
year only had files available up to month 7 at the time of the project.
</p>

<div class="highlight">

<strong>Solution:</strong>
The pipeline logic was adjusted to process available monthly datasets
without stopping the entire pipeline.

</div>


<h3>2. HTTP 403 Forbidden Error</h3>

<p>
Azure Data Factory returned a 403 Forbidden response for unavailable
monthly URLs.
</p>

<div class="highlight">

<strong>Solution:</strong>
The source URL and available months were checked before processing.

</div>


<h3>3. Databricks External Location Conflict</h3>

<pre>
Input path URL overlaps with an existing external location.
</pre>

<div class="highlight">

<strong>Solution:</strong>
Existing external locations were checked and conflicting paths were
removed or reused.

</div>


<h3>4. Azure Storage Permissions</h3>

<p>The following Azure roles were configured:</p>

<ul>

<li>Storage Blob Data Contributor</li>

<li>Storage Account Contributor</li>

<li>Storage Queue Data Contributor</li>

<li>EventGrid EventSubscription Contributor</li>

</ul>


<h3>5. ABFSS Path</h3>

<p>Correct format:</p>

<pre>
abfss://container@storageaccount.dfs.core.windows.net/path
</pre>

<p>Example:</p>

<pre>
abfss://silver@nyctaxideepa.dfs.core.windows.net/
</pre>

</section>



<section>

<h2>📊 Future Power BI Dashboard</h2>

<p>
The Gold-layer data can be used to create interactive Power BI reports.
</p>

<p>Possible KPIs include:</p>

<ul>

<li>Total Taxi Trips</li>

<li>Total Revenue</li>

<li>Average Fare</li>

<li>Average Trip Distance</li>

<li>Trips by Borough</li>

<li>Trips by Taxi Zone</li>

<li>Passenger Count</li>

<li>Payment Type Distribution</li>

<li>Monthly Trip Trends</li>

</ul>

</section>



<section id="learnings">

<h2>🎓 Key Learnings</h2>

<ul>

<li>Building Azure Data Factory pipelines</li>

<li>Using dynamic parameters</li>

<li>Using ForEach activities</li>

<li>Using If Condition activities</li>

<li>Web-based data ingestion</li>

<li>Working with ADLS Gen2</li>

<li>Building PySpark transformations</li>

<li>Working with Azure Databricks</li>

<li>Using Delta Lake and Parquet</li>

<li>Using Managed Identity</li>

<li>Creating Azure Access Connectors</li>

<li>Creating Databricks Storage Credentials</li>

<li>Creating External Locations</li>

<li>Working with Unity Catalog</li>

<li>Building cloud-based ETL pipelines</li>

</ul>

</section>



<section id="contact">

<h2>👩‍💻 Author & Contact</h2>

<h3>Deepa Joshi</h3>

<p>
Aspiring Data Engineer | Data Analyst
</p>

<p>
<strong>GitHub:</strong>
<a href="https://github.com/deepamonger"
target="_blank">
github.com/deepamonger
</a>
</p>

<p>
<strong>Project:</strong>
NYC Taxi Azure Data Engineering
</p>

<p>
<strong>Technologies:</strong>
Azure Data Factory | ADLS Gen2 | Azure Databricks |
PySpark | Delta Lake | Power BI
</p>

</section>


</div>


<footer>

<p>
© 2026 Deepa Joshi
</p>

<p>
NYC Taxi Azure Data Engineering Portfolio Project
</p>

</footer>


