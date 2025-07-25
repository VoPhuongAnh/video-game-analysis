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
    <li>Insight Generation</li>
    <li>What patterns or recommendations emerge?</li>    
    <li>Visualization & Reporting</li>    
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

   ```python
    # Install Kaggle library
    !pip install -q kaggle

    # Upload kaggle.json
    from google.colab import files
    files.upload() # Select and upload your kaggle.json file

    # Create .kaggle directory and set permissions
    !mkdir -p ~/.kaggle
    !cp kaggle.json ~/.kaggle/
    !chmod 600 ~/.kaggle/kaggle.json

    # Verify Kaggle API access
    !kaggle datasets list

    # Using Kaggle CLI to download datasets:
    !kaggle datasets download -d gregorut/videogamesales

    # Unzip the folder:
    !unzip videogamesales.zip

    # Import python libs & load dataframe:
   
    import pandas as pd
     import numpy as np
     import matplotlib.pyplot as plt
     import seaborn as sns

    df = pd.read_csv('vgsales.csv')
    df.head()
   
    ```
   
    Otherwise, You can also download the csv file to local folder to use but this shall need to save the file to colab folder each time of reconnect.


   ```python
    ## From Kaggle API
   
    # Install dependencies:
    !pip install kagglehub[pandas-datasets]

    # Set the path to the file
    file_path = "vgsales.csv"

    # Load the latest version
    df = kagglehub.load_dataset(KaggleDatasetAdapter.PANDAS,"gregorut/videogamesales",file_path)

    print("First 5 records:", df.head())
   ```


3. Data Cleaning
</br> 3.1 Check missing values
</br> We run this code to check total missing values (if any) in each columns:

```python
# Check total null in each columns:
df.isnull().sum()
```

</br> ... so we have the result as: 
        
|              | **Total Missing values**   |
|-------------:|-----|
|     Rank     |   0 |
|     Name     |   0 |
|   Platform   |   0 |
|     Year     | 271 |
|     Genre    |   0 |
|   Publisher  |  58 |
|   NA_Sales   |   0 |
|   EU_Sales   |   0 |
|   JP_Sales   |   0 |
|  Other_Sales |   0 |
| Global_Sales |   0 |
        

</br>3.1a. Handle missing value in Publisher column:

       ```python
            !pip install pandasql
    
            import pandasql
            from pandasql import sqldf
    
            # Use SQL Query to filter all record with NaN in Publisher column from original df:
            # For review only:
    
            query1 = "SELECT * FROM df WHERE Publisher IS NULL"
            publisher_missing_df = sqldf(query1)
            publisher_missing_df.shape[0]
    
       ```

</br> So we have 58 records need to be filled with a proper value. I might check all the different value already have in the Publisher column of the original df

       ```python
            # check if Publisher already have value "Unknown":
            df[df['Publisher'] == "Unknown"]    
       ```
       ```python
            # fill N/a values with "Unknown":
            df['Publisher'].fillna('Unknown', inplace=True)
    
            # Check if the Publisher's missing values are all filled successfully:
            df.isnull().sum()
       ```
</br> Result shall be like:
        
        |  | 0 |
        |---:|---|
        | Rank | 0 |
        | Name | 0 |
        | Platform | 0 |
        | Year | 271 |
        | Genre | 0 |
        | Publisher | 0 |
        | NA_Sales | 0 |
        | EU_Sales | 0 |
        | JP_Sales | 0 |
        | Other_Sales | 0 |
        | Global_Sales | 0 |
        | dtype: int64 |

</br>3.1b. Handle missing value in Year column:
   
There are 2 ways to handle this:

* Remove all the missing year records
* Research for correct info and input to original df one by one.

</br> In order to do the latter: I can think of fill them with the mode of Year column but the result might be affected. Another way is to mass research their correct years. Considering that it takes time to resolve this issue in latter method, I decided to perform the former.

        ```python
        # check total number of records that are missing value in year:
        # for review only:
        
        df[df['Year'].isnull() == True]['Rank'].count()
        
        # drop all records with NaN value in Year column:   
        df2 = df.dropna(subset=['Year'])
        df2
        
        # check total null values in df2:
        df2.isnull().sum()
        
        print("Total record left after handling missing values take " ,round(df2.shape[0]/df.shape[0]*100,2), "% of the total one in original df")
        ```

</br> ... so we already done with removing missing year record in original df. The new dataframe with shall be used for further EDA should be df2.


</br> 3.2 Standardizing formats

</br> Convert dtypes of columns in dataframe:
   
```python
df2.convert_dtypes().dtypes
```

</br>The result showed be as below so all columns are converted to string or numeric types:
   
|              | 0              |
|-------------:|----------------|
|     Rank     |          Int64 |
|     Name     | string[python] |
|   Platform   | string[python] |
|     Year     |          Int64 |
|     Genre    | string[python] |
|   Publisher  | string[python] |
|   NA_Sales   |        Float64 |
|   EU_Sales   |        Float64 |
|   JP_Sales   |        Float64 |
|  Other_Sales |        Float64 |
| Global_Sales |        Float64 |

dtype: object

</br>3.3 Check & Remove duplicates
 
</br>I count duplicated records in dataframe df2 and the result shows that we have no duplicates in this dataframe.
   
    ```python
    # Check total duplicate in df2:
    df2[df2.duplicated()].count()
    ```  
    
   </br>3.4 Handling outliers
4. Correct types and inconsistencies

5. Exploratory Data Analysis (EDA)
</br>5.1. Descriptive analyst

```python
df2.describe()
```

</br> And we have the result as below table:

|       |         Rank |         Year |     NA_Sales |     EU_Sales |     JP_Sales |  Other_Sales | Global_Sales |
|------:|-------------:|-------------:|-------------:|-------------:|-------------:|-------------:|-------------:|
| count | 16327.000000 | 16327.000000 | 16327.000000 | 16327.000000 | 16327.000000 | 16327.000000 | 16327.000000 |
|  mean |  8292.868194 |  2006.406443 |     0.265415 |     0.147554 |     0.078661 |     0.048325 |     0.540232 |
|  std  |  4792.669778 |     5.828981 |     0.821591 |     0.508766 |     0.311557 |     0.189885 |     1.565732 |
|  min  |     1.000000 |  1980.000000 |     0.000000 |     0.000000 |     0.000000 |     0.000000 |     0.010000 |
|  25%  |  4136.500000 |  2003.000000 |     0.000000 |     0.000000 |     0.000000 |     0.000000 |     0.060000 |
|  50%  |  8295.000000 |  2007.000000 |     0.080000 |     0.020000 |     0.000000 |     0.010000 |     0.170000 |
|  75%  | 12441.500000 |  2010.000000 |     0.240000 |     0.110000 |     0.040000 |     0.040000 |     0.480000 |
|  max  | 16600.000000 |  2020.000000 |    41.490000 |    29.020000 |    10.220000 |    10.570000 |    82.740000 |


</br>5.2. Boxplot for numeric columns:

</br>5.2.1. Boxplot for Year column

```python
# Boxplot for 'Year'

bp1 = plt.boxplot(df2['Year']
            , notch=False
            , vert='vertical'
            , orientation='vertical'
            , whis = 1.5
            , meanline=True
            #, showcaps=False # show nút chặn ở 2 đầu
            , showbox=True
            , showfliers=True
            , showmeans=True # Show the arithmetic means
            , labels=['Year'] # show the columns label in X axis
            , patch_artist=True # fill boxplot with colors
            )

# set facecolor for patch_artirst:
patch_colors = ['lightblue']

for patch, color in zip(bp1['boxes'], patch_colors):
  patch.set_facecolor(color)

# plot:
plt.show()
```

</br>5.2.2. Boxplot for Sales columns
</br>5.3. Distribution of data
</br>5.3.1. Hist for the whole df2

```python
df2['Year'].plot.hist(bins=8,
                      alpha=0.5,
                      color='black',
                      edgecolor='white'
                      )
```

</br> ... and so we got the histogram for the df2 as below:


</br>5.3.2. Histogram for in platform and gerne? 

7. Statistical Modeling / Clustering records by sales
   </br>6.1. Correlation coefficients matrix
   </br>6.2. Heatmap visualization
   </br>6.3. Model selection (e.g., regression, classification)
   </br>6.4. Evaluation metrics (e.g., accuracy, R²)
   </br>6.5. Insight Generation
   </br>6.6. What patterns or recommendations emerge?

8. Tie findings to real-world implications
9. Visualizations (histograms, scatter plots, heatmaps) & Reporting
10. GitHub README or selection for presentation
    
<h3>Dependencies </h3>

* pandas==1.5.3
* numpy==1.24.2
* matplotlib==3.7.1

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
