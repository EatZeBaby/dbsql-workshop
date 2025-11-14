# [Part 2: User POV] Databricks SQL in Action: Intelligent Data Warehousing, Analytics, and BI Hands-On Lab

This workshop guide is broken up into **two major sections**:

- **Administrator POV** – for Data Architects, Data Warehousing Architects, and Database Administrators
- **User POV** – for Data Analysts, Business Analysts, SQL Analysts, and similar roles

In this portion of the lab, we will focus on the **User POV** which is the perspective of users who work with data to build dashboards, run queries, and gain insights using Databricks SQL.

We’ll be using the taxi datasets from yesterday  to complete the exercises.

Here’s what we’ll cover in the User POV:

- **Intro:** Navigating Databricks SQL as a Workspace User  
- **Step 1:** Create an AI/BI Dashboard  
- **Step 2:** Publish and Share an AI/BI Dashboard  
- **Step 3:** Create an AI/BI Genie  
- **Step 4:** Publish and Share an AI/BI Genie  
- **Step 5:** Monitoring AI/BI Genie 
- **Step 6:** Evaluating AI/BI Genie
- **Step 7:** View the Entity Relationship Diagram (ERD)
- **Step 8:** View Data Lineage  

Let’s begin with the role of the Workspace User!

## Intro: Navigating Databricks SQL as a Workspace User

Once you’re logged into the workspace, Databricks presents a landing page with unified navigation.

The Databricks workspace offers a user-friendly experience, providing easy access to tools used in data engineering, data science, and analytics workflows. On the left-hand navigation pane, you’ll find a dedicated section for **Databricks SQL**, which includes:

* Creating and running SQL queries using the **SQL Editor**
* Monitoring previous and active **Queries**
* Building visual **Dashboards** for reporting
* Running queries using **Serverless SQL Warehouses**
* Using **Genie**, a natural language interface to analyze data with AI assistance

This intuitive interface allows data analysts, business analysts, and other SQL users to work seamlessly across all aspects of the analytics process.

## Step 1: Create an AI/BI Dashboard

You can use dashboards to build data visualizations and share informative insights with your team. AI/BI Dashboards in Databricks offer:

* AI-assisted authoring
* Enhanced visualization options
* Streamlined configuration tools

These dashboards enable users to quickly turn data into shareable, impactful stories. Once published, dashboards can be shared with anyone who has a Databricks account—even if they don’t have direct workspace access.

### Creating a Dashboard

1. Navigate to the **Dashboards** section from the left-side navigation pane.
2. Click **Create Dashboard** in the top-right corner.
3. Add your dataset by either:

   * Selecting a **table** directly
   * Writing a **SQL query** to define your dataset

For this lab, you will:

* Add the taxi tables and views directly

> **Note:** In a production environment, it’s best to build dashboards on clean Silver or Gold layer data.

### Step 1a: Creating Visualizations
4. Back in the canvas, to make a visualization, click the chart button in the blue bar at the bottom. Drag and drop your chart in any area of choice
5. Before you take advantage of the text-to-viz feature, make sure that your dataset is set to flights_silver_mv
6. Then type "Count of Taxi trips". Click accept.
6b. Then create another viz by typing "taxi trips by day of week". You can edit the bar chart using the right hand navigation pane by:
- adding a description to the bar chart
- changing the visualization type
- editing the groupby colors and labels

7. You can also create your own visualizations manually using the right hand-navigation pane
- select dataset taxi_daily_zone_summary
- select pie visualization type
- title as Count of nb trip
- Angle is count(*)
- Color/Group by Borough 

Feel free to continue playing around with the different visualizations that you can create using natural language or building them manually yourself.
****
## Link to Day 1 Questions
Create visualizations that answers yesterdays questions
- Which zones had the highest yearly revenue? (Top 5)
- Are there any zones with unusual revenue fluctuations?
- Do trip counts correlate with revenue per zone? (Yes/No)

Example of a dashboard
![](/Volumes/main_hec_nov_2025/axel_richier/raw/Screenshot 2025-11-14 at 00.15.25.png)
### Step 1b: Adding Filters
8. AI/BI dashboards also support text widgets using markdown. Add a text widget to your dashboard and title it "Yellow Taxi Data Dashboard"
9. Filters are dashboard widgets that help viewers narrow down results and refine data in visualizations. To add a filter, click the filter button on the blue bar and drag and drop it to an area on your canvas.
10. Select the type of filter as date picker and the field should be a date or timestamp
11. Test out the filter by selecting a date or a date range

### Step 1c: Adding Parameters
Unlike field filters, which directly filter data fields, parameter filters alter the SQL query itself. A filter can be applied to one or more parameters, and parameters must be added to datasets first

12. Go to the data tab and clone another taxi_daily_zone_summary as your data set and rename it to daily_taxi_parameters
13. Remove the semicolon at the end of the SQL statements and add a where clause and then description =
```sql
SELECT * 
FROM taxi_daily_zone_summary 
WHERE Borough = :parameter
```
14. Then click the add parameter button, click the gear button and change the display name to destination and the parameter Type to string
15. Type Manhattan in the parameter box to make sure it works and run the query again

## Step 1d: Filtering on Parameters

Dashboards become much more powerful and user-friendly when they allow interactivity. One way to do this is by filtering data using parameters.

### Add a Parameter Filter to Your Dashboard

1. Go to your dashboard canvas.
2. Click the **Add Filter** button on the blue toolbar.
3. Drag and drop the filter widget onto the canvas near your visualizations.
4. Set the filter type to **Single Value**.
5. For the data source, choose your `taxi_daily_zone_summary` table.
6. For the filter field, select **Destination**.
7. Under the **Parameters** section, link this filter to the parameter you previously created. It should be named `flights_silver_parameters.destination`.
8. Enter a Borough in the filter box (e.g., `Bronk`, `Queens`, `Manhattan`) and watch your dashboard dynamically update based on the selection.

---

## Cross-Filtering

AI/BI Dashboards also support **cross-filtering**, a powerful feature that lets users explore data interactively:

* Simply **click on a value** (e.g., a bar in a chart or a segment in a pie chart).
* All other visualizations on the same dataset will automatically filter based on the selected value.
* This allows users to drill down into subsets of data and discover patterns across multiple visuals in real time.

> **Note:** If your dashboard contains **multiple pages**, you can also apply **global filters**.
>
> Global filters apply across all pages, affecting any visualizations that use the same dataset.

Cross-filtering and parameters make your dashboards feel alive, allowing end users to explore and gain insights on their own without writing a single line of SQL.

### Step 2: Publish and Share an AI/BI Dashboard

Publish a dashboard to create a clean copy of the current draft. You must have at least CAN EDIT permissions to publish a dashboard.

When you publish a dashboard, you can choose to embed your credentials or not:

* **Embed credentials**: All viewers of a published dashboard can run queries using your credentials for data and compute. This allows users to see the dashboard even if they don’t have access to the originating workspace, underlying data, or SQL warehouse. *This might expose data to users who have not been granted direct access to it.* This is the default option.

* **Don’t embed credentials**: All viewers of the published dashboard run queries using their own data and compute credentials. To view results in the dashboard, viewers need access to the workspace, the attached SQL warehouse, and the associated data.

For this workshop we will:

1. Give the dashboard a title: **Taxi Data Dashboard**
2. Embed the credentials
3. Click **Publish**

After publishing, we can now give privileges to users or groups in our organization to manage, edit, run, or view the dashboard. Additionally, AI/BI Dashboards can now be **embedded into external websites and applications**, a common request among customers.

###Step 2a: Ask Genie in Dashboards

Within any published AI/BI Dashboard, users can use the built-in **Ask Genie** feature to explore their data in a natural, conversational way.

To ask Genie about a specific dashboard chart:
* Click Ask Genie from a Genie-enabled published dashboard.
* Click a dashboard chart to select it. Genie displays the selected chart title in the chat window.
* Ask questions about the data represented in the selected chart.

This is a great way to dig deeper into specific insights that the visualizations may not directly reveal.

#### Why Create a Dedicated Genie Space?

While you can use **Ask Genie** inside the dashboard, it is limited to the datasets and visualizations used in that dashboard.

If you want to:

* Ask more detailed or broad questions
* Explore multiple tables not used in the dashboard
* Conduct ad hoc analysis and save reusable queries

Then it's best to **create a dedicated Genie Space** where you can access your full data catalog and generate richer insights across different datasets.

**Next up: Let's explore how to create and share an AI/BI Genie Space.**

### Step 3: Create a AI/BI Genie

AI/BI Genie is a no-code interface powered by AI with data intelligence that allows business users to conduct self-serve data analytics using natural language. Domain experts, such as data analysts, configure Genie spaces with datasets, sample queries, and text guidelines to help Genie translate business questions into analytical queries. After set up, business users can ask questions and generate visualizations to understand operational data. You can continuously update Genie’s semantic knowledge as your data changes and users pose new questions. 

1. You can create a Genie from a table in the catalog explorer, from the Genie listing page or from a dashboard. For this workshop we will create a Genie the Genie listing page
2. Click on Genie on the left hand navigation pane and click new
3. Give the Genie the title "Taxi Data Genie"
4. Description should say "for users to understand and gather insights on taxi data from the year 2025"
5. Select a warehouse.  
6. Add your tables 
  - **Note:** Layer views to reduce the number of columns and add use-case-specific information to increase response quality; and only bring in the tables and columns needed to answer questions for a given domain
7. You can optionally add sample questions that you know other users are bound to ask consistently... 

Your genie space is now created. Let's start chatting and teaching genie.

### Genie Space Overview
Before we start working with Genie. Let's take a look at how the Genie is organized.

On the left you can see different icons. 
- **Chat:** Currently, we are in the chat window. This is where Genie interactions take place
- **Instructions:** Instructions help to guide Genie’s responses so that it can process the unique jargon, logic, and concepts in a given domain. Comprehensive instructions are critical to a seamless, intuitive Genie space experience. To enter instructions, click Instructions icon Instructions in the Genie space sidebar to open the instructions pane. Use this pane to add General instructions, Example SQL Queries, and SQL Functions.
  - [General Instructions](https://docs.databricks.com/en/genie/index.html#general-instructions): Provide plain text instructions that clearly convey your business or response preferences for Genie to follow. You can format the instructions as a single comprehensive note or categorize them by topics for better organization. For example: "Our fiscal year starts in February"
  - [Example SQL Queries](https://docs.databricks.com/en/genie/index.html#example-sql-queries): are SQL queries that you prepare to help train Genie. When you add example queries, you are effectively showing Genie how to use your data to answer questions. You can also add example questions to teach Genie about the kinds of questions you would expect the example query to answer.
  - [SQL Functions](https://docs.databricks.com/en/genie/index.html#sql-functions): are custom functions that are stored in Unity Catalog and used by Genie to answer specific questions that include complex arguments or calculations that Genie should not be able to access or edit 

- **Data:** shows the tables that power the space and the metadata associated with them
- **Monitoring:** shows the history of activities within your space
- **Benchmarks:** help you evaluate the accuracy of your Genie space
- **Settings:** brings you back to the Genie form where you can edit the creation of the Genie space

%md
### Step 3a: Chatting with Genie

1. Click on "explain the dataset"
2. Genie quickly responds. Now ask "Which zones have the most trip in september? Give me the top 3 by average nb of trips"
3. Genie should give you an appropriate answer 
4. You can click "show generated code" to see the underlying SQL code that Genie leveraged to create a response. You can optionally edit it directly if you are a SQL expert and understand the code.
5. Open instructions tab and see the example queries section with where you can add sample queries for Genie to reuse. 
7. Genie can even create quick visualizations for you to better understand your insights. Let's ask genie: "Now graph this as a bar chart sorted most to least trips"

## Test Day 1 Questions:
Again, let's try to answers these question with Genie :


## Link to Day 1 Questions
Create visualizations that answers yesterdays questions
- Which zones had the highest yearly revenue? (Top 5)
- Are there any zones with unusual revenue fluctuations?
- Do trip counts correlate with revenue per zone? (Yes/No)

Now, you can see how powerful Genie can be when you compare how we retrieved this answers :
1- From an exploratory notebook, without Data Quality Guaranty
2- From a dashboard, hoping that there is actually a chart that answers the data, and needs you to interpret it.
3- From just a natural question, in a matter of seconds.

![](/Volumes/main_hec_nov_2025/axel_richier/raw/Screenshot 2025-11-14 at 00.20.14.png)

### Step 4: Share Genie
Now that your Genie space has been created and you have tested it by chatting and teaching Genie, it is now time to share Genie with the rest of your team

1. You can specify certain users or groups to share with at a given permission level: CAN MANAGE, CAN EDIT, CAN RUN, and CAN VIEW
2. Use the Copy link button at the bottom of the Share dialog to get a shareable link to the Genie space. Privileged users can click the link to open the Genie space in a new tab and ask questions.

### Step 5: Monitoring Genie

As users begin to ask Genie questions, they are able to provide feedback responses using a thumbs-up or thumbs-down feedback button. On the monitoring page, you can view individual questions and responses, thumbs-up or thumbs-down feedback provided by users, and questions marked for review. 

1. Head back to the chat window and select the chat monitoring to view our conversation with Genie
2. Scroll down to the last prompt we asked Genie "Which airlines are delayed the most? Give me the top 5 by average delay" and give that a thumbs up
3. Head back to the monitoring page to verify our feedback response has been recorded

**The monitoring page** shows all of the questions and answers that have been asked in the space. You can filter questions by time, rating, user, or status. By monitoring the space, Genie space editors can proactively understand the queries raised by business users and how the Genie space responded.

By identifying the questions that Genie struggles with, you can update the Genie space with specific instructions to improve its responses. Click a question to open the question and response text. You can also access the complete chat thread from this view.

### Step 6: Evaluating Genie

Benchmarks allow you to systematically evaluate Genie’s performance at answering business questions in a structured, measurable way. Unlike instructions, benchmarks are not used to guide or inform Genie—they are strictly used to test accuracy and reliability.

Benchmarks help you:

* Scale up testing of Genie’s responses
* Measure accuracy using expected SQL queries
* Track performance over time

When setting a benchmark, you provide:

* A **question** you want Genie to answer
* An **SQL query** that represents the expected correct answer

Genie will generate its own answer to the benchmark question and run it. The results are then compared to your provided SQL query to calculate a score.

Let’s walk through how to create a benchmark:

1. In your Genie space, click the **Benchmarks** tab in the left sidebar
2. Click the **Questions** tab, then select **Add Benchmark**
3. In the question field, enter:

   > "How many taxi trips in the Queens borough on July 14th ?"
4. Below is the correct SQL statement to answer the question. Copy and paste it into the SQL field:

```sql
SELECT
  SUM(`nb_trip`) AS total_trips
FROM
  `main_hec_nov_2025`.`<your_schema>`.`taxi_daily_zone_summary`
WHERE
  `Borough` = 'Queens'
  AND `pickup_date` = '2025-07-14';
```

5. Click **Preview** to run the query and verify the expected result is **15 403 trips** in the Queens on July 14th 2025.
6. Once verified, you can add more variations of the same question that you believe people will ask, or you've heard them ask.   

7. Now, click **Run Benchmark** to test Genie’s response against the correct answer. If Genie’s output matches your ground truth result (15 403), the benchmark score will be marked **100% accurate**.

Benchmarks are a great way to validate Genie’s ability to answer complex questions using multiple tables, ensuring reliability before sharing results with stakeholders.

### Step 7: Viewing Entity Relationship Diagram

Back in the catalog explorer, you will see that our foreign key constraint has been labeled, but better yet, Databricks supports creating/visualizing entity relational models with primary keys/foreign keys in an Entity relationship digram within the Catalog Explorer UI. 

1. Navigate back to the catalog explorer
2. Locate your catalog
3. Locate your schema
4. Select the flights_bronze table
5. Click on view relationships

### Step 8: Viewing Data Lineage

In the catalog explorer, we can also view lineage graphs for each table to see all the upstream and downstream tables.


1. On the flights table, click lineage
  - Here we can see the upstream/downstream tables and a list of workflows, dashboards, and queries that the table is used in
2. To view the lineage diagram click on "see lineage graph"
  - Here you can see a visual representation of the data lineage flow from each data or AI asset
