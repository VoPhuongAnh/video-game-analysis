# Project name: video-game-analysis

<h2> 🗂️ Project Overview </h2>

📌 Title: Video Game Analysis (2018 - 2020)

<h2>📄 Objective: </h2>
Purpose of this project:
This project is aiming to uncover trends in publishing of video game  analyzed by publishers, platforms and genres over years. This analysis is also look into the sales of them in specifics areas and in global scale.


<h2> 📊 Dataset Description: </h2>

<h3>Briefly describe:</h3>  

Source : This dataset is found at Kaggle. You can access to dataset via this link : 

<a href = "https://www.kaggle.com/datasets/gregorut/videogamesales/data" target="_blank" style="
    display:inline-block;
    padding: 10pax 20pax;
    background-color: black;
    color: white;
    font-family: Arial, san-serif;
    boder-radius: 3px;
    transition: background-color 0.3s ease"> Click here </a>

Format:  CSV file 

<h3> Format and size </h3>  

- Dataset Format:  CSV file
- Size: 1.36 MB
- Dataset contains 11 columns with total of 16,598 records.

<h2>🧪 Project Structure</h2>
<h3>📁 Folder Organization:</h3>

The project contain such folders as below:
<details>
  <summary>📦 data-analysis-project/</summary>
  <ul>
    <li>├── data/               # Raw and cleaned datasets</li>
    <li>├── notebooks/          # Jupyter/Colab notebooks</li>
    <li>├── src/                # Python scripts and functions</li>
    <li>├── reports/            # Visualizations and analysis summaries</li>
    <li>├── docs/               # Project documentation</li>
    <li>└── README.md           # Project overview and instructions</li>
  </ul>
</details>

<h3>🔍 Steps in Data Analysis</h3>

<details>
  <summary>Details</summary>
  <ul>
    <li>Data Collection</li>
    <li>Import datasets</li>
    <li>Handle missing data</li>
    <li>Perform exploratory checks</li>
    <li>Data Cleaning</li>
    <li>Remove duplicates</li>
    <li>Correct types and inconsistencies</li>
    <li>Normalize or transform variables</li>
    <li>Exploratory Data Analysis (EDA)</li>
    <li>Summary statistics</li>
    <li>Correlation matrix</li>
    <li>Visualizations (histograms, scatter plots, heatmaps)</li>
    <li>Feature Engineering</li>
    <li>Create new variables</li>
    <li>Select important features</li>
    <li>Statistical Modeling / Machine Learning (Optional)</li>
    <li>Model selection (e.g., regression, classification)</li>
    <li>Evaluation metrics (e.g., accuracy, R²)</li>
    <li>Insight Generation</li>
    <li>What patterns or recommendations emerge?</li>
    <li>Tie findings to real-world implications</li>
    <li>Visualization & Reporting</li>
    <li>Use Matplotlib, Seaborn, Plotly, or Tableau</li>
    <li>Generate charts for GitHub README or presentation</li>
  </ul>
</details>

<h2>📘 Documentation</h2>
<h3>**Project goals**</h3>

<h3>Data glossary</h3>

 - _rank_: the order of each game in this record, which is based on their total sales
 - _title_: the official name of a video game. It’s a reflection of the game’s theme, story, genre, and tone
 - _platform_: the system or environment where video games are played, developed, and distributed. It can be hardware-based (like consoles or PCs) or software-based (like cloud services or digital marketplaces)
 - _genre_: a category that defines a video game based on its gameplay mechanics, not its story, setting, or graphics. It’s all about how you interact with the game — what you do, how you do it, and what kind of challenges or experiences it offers
 - _publisher_: a company responsible for bringing video games to market — they handle the business side so developers can focus on creating the game itself
 - _NA_Sales_ : Sales in North America (in millions)
 - _EU_Sales_ : Sales in Europe (in millions)
 - _JP_Sales_ : Sales in Japan (in millions)
 - _Other_Sales_ : Sales in the rest of the world (in millions)
 - _Global_Sales_ : Total worldwide sales

<h3>How to reproduce results</h3>

1. Data Collection:

   This data is available in Kaggle so that I skip the step of collecting data

2. Import datasets:

    In this project, I use python script to  download the dataset using Kaggle API. The script is as below:
   
    You can also download the csv file to local folder to use.

3. Handle missing data:

   There are some records which null values in Year column. There are 2 solutions to solve this issue, that are remove all records with years are missing or fill them with a proper value.
   In order to do the latter: I can think of fill them with the mode of Year column but the result might be affected. Another way is to mass research theỉ correct years. 

5. Perform exploratory checks
6. Data Cleaning
7. Remove duplicates
8. Correct types and inconsistencies
9. Normalize or transform variables
10. Exploratory Data Analysis (EDA)
11. Summary statistics
12. Correlation matrix
13. Visualizations (histograms, scatter plots, heatmaps)
14. Feature Engineering
15. Create new variables
16. Select important features
17. Statistical Modeling / Machine Learning (Optional)
18. Model selection (e.g., regression, classification)
19. Evaluation metrics (e.g., accuracy, R²)
20. Insight Generation
21. What patterns or recommendations emerge?
22. Tie findings to real-world implications
23. Visualization & Reporting
24. Use Matplotlib, Seaborn, Plotly, or Tableau
25. Generate charts for GitHub README or presentation
    
<h3>Dependencies (requirements.txt)</h3>
upcoming
<h3>Contribution guidelines (if collaborative)</h3>

If you find this analysis ineresting and would like to give your feedbacks for better improvement, please feel free to let me know via email chansoo194@gmail.com 

<h2>🚀 Extras Info </h2>  

What is the correlation between NA_sales, EU_sales, JP_sales, Other_Sales và Global_sales?

From the columns, we can see that game market is devided into 4 submarkets: NA, EU, JP and other areas. So my questions is that whether there were any games that are performed well in other markets, rather than the 3 biggest ones?

In order to answer this questions, I will devide the filtered records inot 2 groups :
    
    - Group 1: table include such games have better Other_sales than the 3 markets. How many games (in total) falls into this group? Which publishers. platform and genre have the biggest sales in this table?
    - Group 2: table include the rest, which sales mainly from either NA, EU or JP. I might think of clustering these records based on 3 variables: NA_sales, EU_sales, JP_sales. Method for clustering could be K-mean clustering.

<h3>Interactive reports :</h3>
To review the interactive report for key insights visualization, please visit my dashboard in Looker Studio via this link: 

<a href="https://lookerstudio.google.com/reporting/09d88ddb-5d3c-47ca-9198-db9b3f2a6694" target="_blank">Report</a>

Automated reporting with scripts : (Upcoming)
