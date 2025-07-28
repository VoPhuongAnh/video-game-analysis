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
   
</br> Otherwise, You can also download the csv file to local folder to use but this shall need to save the file to colab folder each time of reconnect.


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
</br> 3.1 Check missing values:
</br> We run this code to check total missing values (if any) in each columns:

```python
# Check total null in each columns:
df.isnull().sum()
```

</br> ... sothe result is as below table, which means we have 2 columns with missing values: Year columns has 271 missing values while the Publisher column has 58 ones. Other columns seem to be fine.  
        
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
        

</br> 3.1a. Handle missing value in Publisher column:

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
| dtype: int64 | |

</br> So the total of Publisher is now 0 , means we get replaced all the missing values in Publisher columns with 'Unknown' value. This action, in fact, shall increase the total count of unknown publisher games but it's still ok for our further analysis.

</br>3.1b. Handle missing value in Year column:
   
There are 2 ways to handle this:

* Remove all the missing year records
* Research for correct info and input to original df one by one.

</br> In order to do the latter, the solution I think of is to fill them with the mode of Year column but the result might be affected. Another way is to mass research their correct years. Considering that it takes time to resolve this issue in latter method, so that I decided to perform the former.

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
The result so that there is no duplicates in our df2
    
</br>3.4 Handling outliers

In order to chec the outliers value, I might want to see the Min and Max values of each columns in the df2

```python
# check numeric columns from df2:
numeric_columns = df2.select_dtypes(include=['number']) # or df2.select_dtypes('number')

# find min and max of each colums:
df2_numeric_min_df = numeric_columns.min().to_frame().reset_index()
df2_numeric_max_df = numeric_columns.max().to_frame().reset_index()

df2_numeric_stats = pd.merge(df2_numeric_min_df,df2_numeric_max_df,on="index", suffixes=('min','max'))

df2_numeric_stats.rename(columns={'index':'column_name','0min':'min','0max':'max'}, inplace=True)
df2_numeric_stats

```

</br> And I combine Min and Max value of each column to a consolidated table to have a closer look on them:

|   |  column_name |     min | max      |
|--:|-------------:|--------:|----------|
| 0 |         Rank |    1.00 | 16600.00 |
| 1 |         Year | 1980.00 |  2020.00 |
| 2 |     NA_Sales |    0.00 |    41.49 |
| 3 |     EU_Sales |    0.00 |    29.02 |
| 4 |     JP_Sales |    0.00 |    10.22 |
| 5 |  Other_Sales |    0.00 |    10.57 |
| 6 | Global_Sales |    0.01 |    82.74 |

</br> then I might want to see the Mean value of each columns also, together with the Max and Min:

```python
numeric_columns.agg(['min', 'max','mean'])
```
</br> and now the table might be looked like this:

|      |      Rank    |    Year     |  NA_Sales |  EU_Sales | JP_Sales    |  Other_Sales |Global_Sales|
|-----:|-------------:|------------:|----------:|----------:|------------:|-------------:|-----------|
|  min |     1.000000 | 1980.000000 |  0.000000 |  0.000000 |    0.000000 |     0.000000 |  0.010000 |
|  max | 16600.000000 | 2020.000000 | 41.490000 | 29.020000 |   10.220000 |    10.570000 | 82.740000 |
| mean |  8292.868194 | 2006.406443 |  0.265415 |  0.147554 |    0.078661 |     0.048325 |  0.540232 |

</br> So here, it looks like that the average values of sales columns seem to be very small which are under 1; while the maximum are very high. Generally speaking, we can imagine that there is a significantly diversification in the sales of games at each regional markets. However, it's not ideally to remove all the high volume sales as outliers since we cannot ignore the well-performed game titles in the whole picture. 

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
<img width="561" height="413" alt="Image" src="https://github.com/user-attachments/assets/d2504e5e-7d16-42c3-9173-c90c4e510c30" /><img src=''>


</br>5.2.2. Boxplot for Sales columns

```python
# boxplot for sales columns:

boxplot_columns = [df2['NA_Sales'],	df2['EU_Sales'],	df2['JP_Sales'],	df2['Other_Sales']]
labels = ['NA_Sales',	'EU_Sales',	'JP_Sales',	'Other_Sales']

flierprops = dict(marker='o',
                  markerfacecolor='lightblue',
                  markersize=8,
                  markeredgecolor='black')

fig, ax = plt.subplots(figsize=(10, 60))

bp = ax.boxplot(boxplot_columns,
           labels=labels,
           patch_artist=True,
           flierprops=flierprops #this is for filling the box
           )

# Define lists of colors for each part
box_colors = ['#FFC0CB', '#ADD8E6', '#90EE90', '#FFD700'] # Pink, Light Blue, Light Green, Gold
median_colors = ['darkred', 'darkblue', 'darkgreen', 'darkgoldenrod']
whisker_colors = ['red', 'blue', 'green', 'orange']
flier_colors = ['purple', 'black', 'darkcyan', 'brown']


# color for boxes:
for patch, color in zip(bp['boxes'], box_colors):
  patch.set_facecolor(color)
  patch.set_edgecolor('black')

# color for median:
for median, color in zip(bp['boxes'], median_colors):
  median.set_color(color)
  median.set_linewidth(2.5)


# color for whisker:
for whisher, color in zip(bp['boxes'], whisker_colors):
  whisher.set_color(color)
  whisher.set_linewidth(1.5)
  whisher.set_linestyle('-')

# color for fliers:
#for flier, color in zip(bp['boxes'], flier_colors):
  #flier.set(marker='x', color=color, alpha=0.7)

# set title & labels:
ax.set_title('Sales by regions')
ax.set_xlabel('Columns')
ax.set_ylabel('Values')

# set gridline:
plt.grid(linestyle='--',
         color='gray',
         alpha=0.7
         #, axis='y'
         )

# plot the boxes:
plt.show()

```

<img width="841" height="4705" alt="Image" src="https://github.com/user-attachments/assets/1f35654f-44dd-49ca-a13a-7d02fd4b60ca" />



</br>5.3. Distribution of data
</br>5.3.1. Hist for the whole df2

```python
mean_year = df2['Year'].mean()

plt.hist(df2['Year'],
         bins=8,
         color='pink',
         edgecolor='black',
         #stacked=True,
         #alpha=0.5,
         cumulative=False,
         align='mid', # bars are centered between the bin edges.

         )

plt.xlabel('year')
plt.ylabel('Frequency')
plt.title('Distribution of data')

#plt.legend()

# ax.axvline(mean_year, color='red', linestyle='--', linewidth=1.5, label='Mean of year')

plt.show()
```

</br> ... and so we got the histogram for the df2 as below:

<img width="580" height="455" alt="Image" src="https://github.com/user-attachments/assets/29664ab0-4446-4a6d-ba73-5ee511e88c1c" />

</br> So from the histogram above, we might have 3 bins of years that most of our data fall into. By running codes to calculate the % of data we have in period 2000-2015:

```python
# or we can calculate the % of data in period 2000-2015:
filter_2000_2015 = df2[df2['Year'].between(2000,2015)].shape[0] #by default : incldusive="both" which means (2000 <= Year <= 2005)
print('% data distribution in period 2000 to 2015: ', round(filter_2000_2015/(df2.shape[0])*100, 2), "%")
```

</br> % data distribution in period 2000 to 2015:  85.78 %

</br> In smaller scall, I want to see how much percentage of my our data falls into the 3 bins: 2000 to 2005, 2005 to 2010 and 2010 to 2015.

```python
distribution_2000_2005 = (df2[(df2['Year'] >= 2000) & (df2['Year'] < 2005)].shape[0]) / df2.shape[0] * 100
distribution_2005_2010 = (df2[(df2['Year'] >= 2005) & (df2['Year'] < 2010)]
  .shape[0]) / df2.shape[0] * 100
distribution_2010_2015 = (df2[(df2['Year'] >= 2010) & (df2['Year'] < 2015)]
  .shape[0]) / df2.shape[0] * 100

# % data in period 2000 to 2005, in comparison to total df2:
print('% data distribution in period 2000 to 2005: ', round(distribution_2000_2005, 2), "%")

# % data in period 2005 to 2010, in comparison to total df2:
print('% data distribution in period 2005 to 2010: ', round(distribution_2005_2010, 2), "%")

# % data in period 2005 to 2010, in comparison to total df2:
print('% data distribution in period 2010 to 2015: ', round(distribution_2010_2015, 2), "%")
```

</br> % data distribution in period 2000 to 2005:  19.59 %
</br> % data distribution in period 2005 to 2010:  36.81 %
</br> % data distribution in period 2010 to 2015:  25.62 %

</br>5.3.2. Histogram for in platform and gerne? 

```python
len(df2['Genre'].unique())
```

</br> We have total of 12 columns for Genre in this dataset

```python
platforms = df2['Platform'].unique()
genres = df2['Genre'].unique()

sns.displot(data=df2,
            x='Year',
            #row='Platform',
            col='Genre',
            kind='hist',
            bins=8,
            height=3,
            aspect=1.2,
            palette='viridis',
            edgecolor='white',
            col_wrap=4
            )
```

<img alt='Histogram-genre' src='docs/genre histograms.png'>

</br> Check the histogram for Platform 

```python
len(df2['Platform'].unique())
```

```python
# Histogram of data distribution over years devided by platforms:

Platform = df2['Platform'].unique()

sns.displot(data=df2,
            x='Year',
            #row='',
            col='Platform',
            kind='hist',
            bins=8,
            height=3,
            aspect=1.2,
            palette='viridis',
            edgecolor='white',
            col_wrap=5
            )
```

<img alt='Histogram-Platform' src='docs/Platform Histograms.png'>

</br> So from the plots we can see that there is a variety in the distribution of data points in years. A number of games in the dataset have a very low publication count, which obscures the details on the histogram.



6. Statistical Modeling / Clustering records by sales
   </br>6.1. Correlation coefficients matrix
   </br>6.2. Heatmap visualization
   </br>6.3. Model selection (e.g., regression, classification)
   </br>6.4. Evaluation metrics (e.g., accuracy, R²)
   </br>6.5. Insight Generation
   </br>6.6. What patterns or recommendations emerge?

7. Tie findings to real-world implications
8. Visualizations (histograms, scatter plots, heatmaps) & Reporting
9. GitHub README or selection for presentation
    
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
