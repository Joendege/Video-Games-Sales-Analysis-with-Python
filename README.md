# Video Games Sales Analysis

## Table of Contents
- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
- [Exploratory Data Analaysis](#exploratory-data-analaysis)
- [Data Analysis](#data-analysis)
- [Recommedations](#recommedations)
- [Results and Findings](#results-and-findings)
- [Limitations](#limitations)
- [References](#references)

---

### Project Overview
This data analysis project aims to provide insights into sales performance of video games over years. By analyzing various the data we seek to indentify trends over the different years, make data driven recommedations and gain a deeper understanding of the video games industry.

#### Global Sales Per Year

![global_sales_yearly](https://github.com/Joendege/Video-Games-Sales-Analysis-with-Python/assets/123901910/22473f80-c6ba-4b25-a44c-6e293da1d24b)

#### Games Released by Year
![games_by_genre](https://github.com/Joendege/Video-Games-Sales-Analysis-with-Python/assets/123901910/28eed397-c695-476c-86a9-1903f64b8f9c)

#### Best Platform Yearly by Sales

![best_platform_yearly_by_sales](https://github.com/Joendege/Video-Games-Sales-Analysis-with-Python/assets/123901910/db7a1cb1-4664-4b0b-a1f3-f1c5b5293d93)


### Data Sources
Sales Data: The primarly data source used for analysis is the "vgsales.csv" file containing details of each video game sales.

### Tools
- Jupyter Notebook - Data Cleaning, Data Analysis and Report Creating [Download Here](https://www.anaconda.com/installation-success?source=installer)

### Data Cleaning and Preparation
In the initial data preparation I performed the following tasks:
- Data loading and Inspection
- Handling null values
- Data cleaning and formartting

### Exploratory Data Analaysis
EDA involved exploring the sales data to answer key questions, such as:
1. Which genre games have been sold the most? Which are the top five genres by games released?
2. Which genre games has the highest sales globally? Which genre has been released/sold most in a single year
3. Which year has the highest sales worldwide?
4. Which are the top publishers by games sold/sales? Which is the top publisher by count each year?
5. How is total revenue distribution by region? How is regional sales comparision by genre?

### Data Analysis

``` Python Pnndas
yearly_genre_count= df.groupby(['Year', 'Genre']).size().reset_index(name= 'Total Games')
year_max_id= yearly_genre_count.groupby('Year')['Total Games'].transform('max') == yearly_genre_count['Total Games']
year_max_genre= yearly_genre_count[year_max_id].reset_index(drop= True)
year_max_genre.drop_duplicates(subset=['Year', 'Total Games'], keep= 'last', inplace= True, ignore_index= True)
year_max_genre
```
```Python Plotly Express
fig= px.bar(reg_genre_sales, 
            x= 'Genre', 
            y= ['Total NA_Sales', 'Total EU_Sales', 'Total JP_Sales', 'Total Other_Sales'], 
            title= 'Regional Sales by Genre', 
            labels= {'value': 'Total Sales'},
            barmode= 'group')

fig.update_layout(
    width= 1100, 
    height= 750, 
    bargap= 0.2)
fig.write_image('regional_sales_by_genre.png')
fig.show()
```

### Recommedations
Based on the analysis we recommed the following action:
- Invest in promotions and marketing in JP and Other region to increase the sales volume
- Focus on promoting the platforms with total sales less that $15.00 M.
- Genre segmentation per region to find out of any increased revenue.

### Results and Findings
The analysis results are summarized as follows:
- The global sales has been increasing steadly and was highest in the from year 2006 to 2010 where after this it dropped steadily.
- Actions and Sports genre have had the highest game produced
- Most games were produced in the from the year 2006 to 2010
- North America sales has been the highest even when segmented by genre.

### Limitations
The records that had null values in the publisher columns i had to drop then, but the year column null values I had to impute with 2 n-neighbours

### References
1. [Pandas Documentation](https://pandas.pydata.org/pandas-docs/stable/reference/frame.html)
2. [Matplotlib Documentation](https://matplotlib.org/stable/api/pyplot_summary.html)
3. [Plotly Express Documentation](https://plotly.com/python/)
4. [Stack Overflow](https://stackoverflow.com/questions/14657241/how-do-i-get-a-list-of-all-the-duplicate-items-using-pandas-in-python)

