# Introduction 

In today's data-driven world, the demand for skilled professionals in data-related roles has grown exponentially. As organizations increasingly rely on data to make informed decisions, understanding the skills required for these roles has become crucial. This project aims to analyze the most in-demand and highest-paying skills for data professionals, with a focus on Data Analysts. By leveraging Python and data visualization techniques, this project provides insights into the skills that are essential for career growth and optimization in the data industry.

# Background

The field of data analytics has evolved significantly over the years, with new tools and technologies emerging to meet the growing complexity of data. Data Analysts play a pivotal role in interpreting and visualizing data to uncover actionable insights. However, the skills required for this role vary widely depending on industry trends and job market demands. This project was undertaken to bridge the gap between aspiring data professionals and the skills they need to succeed. By analyzing job postings and salary data, this project identifies the most in-demand and highest-paying skills, helping learners and professionals prioritize their learning journey.

# Tools I used

This project utilized a variety of tools and libraries to analyze and visualize data effectively:

**Python:** The primary programming language used for data analysis and visualization.

**Pandas:** For data manipulation and cleaning.

**Matplotlib:** For creating static, interactive, and publication-quality visualizations.

**Seaborn:** For advanced data visualization and statistical graphics.

**AdjustText:** To adjust overlapping text in scatter plots for better readability.

**Jupyter Notebook:** For interactive coding and documentation.

**Microsoft Excel:** For initial data exploration and formatting.

**Matplotlib Ticker:** For formatting axes and customizing visualizations.

**VS Code:** The integrated development

# The Analysis

## 1. What the the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. this query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View my notebook with detailed steps here:

[2_skills_Demand.ipynb](3_Project\2_Skills_Demand.ipynb)

### Visualize Data 

```  Python
fig, ax = plt.subplots(len(job_titles),1,figsize=(10,10))

sns.set_theme(style='ticks')

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short']==job_title].head(5)
    #df_plot.plot(kind='barh',x='job_skills',y='skill_perc',ax=ax[i],title=job_title)

    sns.barplot(data=df_plot, x='skill_perc', y='job_skills', ax=ax[i], hue='Skill_count', palette='dark:b_r')

  
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].legend().set_visible(False)
    ax[i].set_xlim(0, 78)

    # JOB TITLE
    ax[i].text(0.5, 1.1, job_title, ha='center'
    , va='center', transform=ax[i].transAxes, fontsize=12)
    

    for n, value in enumerate(df_plot['skill_perc']):
        ax[i].text(value + 1, n, f'{value:.1f}%', va='center')

    if i!=len(job_titles)-1:     
        ax[i].set_xticks([])
    
fig.suptitle('Likelihood of Skills Requested in US Job Postings', fontsize=15)
plt.tight_layout(h_pad=0.5)
plt.show()
```

### Results 

![Vizualization of top skills for Data Nerd](3_Project\images\skill_demand_all_data_roles.png)

 ### Insights 

 - Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists (72%) and Data Engineers (64.9%).

 - SQL is the most requested skills for Data Analysts and Data Scientists, with it in over half the job postings for both roles. For data Engineers, python is the most sought-after skill, appearing in (64.9%) of job postings.

 - Data Engineers require more specialized technical skills (AWS, Azure, Spark) compare to Data Analyst and Data Scientists who are expected to be proficient in more general data management and analysis tools (Excel, Tableau)    


## 2. How are in-demand skills trending for Data Analysts?

### Visualize Data 

```python
df_Plot = df_DA_percent.iloc[:, :5]

sns.lineplot(data=df_Plot, dashes=False, palette='tab10')
sns.set_theme(style='ticks')
sns.despine()

plt.title('Trending Top Skills for Data Analyst Jobs in the US')
plt.xlabel('2023')
plt.ylabel('likelihood in job posting')
plt.legend().remove()


from matplotlib.ticker import PercentFormatter
ax= plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

for i in range(5):
    plt.text(11.2, df_Plot.iloc[-1, i], df_Plot.columns[i], fontsize=9, color='black')


plt.show()
```

### Results

![Trending Top Skills for Data Analysts in the US](3_Project\images\top_skill_demand_image.png)

*Bar graph Visualizing the trending top skills for data analysts in the US in 2023.*

### Insights:

- SQL Dominance: SQL continues to be the most in-demand skill for Data Analysts, maintaining a strong presence in job postings throughout 2023. This highlights its importance as a foundational skill for data-related roles.

- Python's Growing Popularity: Python shows a steady upward trend, reflecting its increasing adoption for data analysis, automation, and machine learning tasks in the industry.

- Specialized Tools Lagging: Other specialized tools or skills (e.g., Tableau, Excel) show relatively lower demand compared to SQL and Python, indicating a preference for versatile and widely applicable skills in the job market.


## 3. How well do jobs and skills pay for Data Analysts?

### Salary Analysis for Data Nerds 

### Visualize Data 
```python 

sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=Job_order, palette='viridis', legend=False)

plt.xlabel('Year Salary ($USD)')
plt.ylabel('')
plt.suptitle('Salary Distribution in the United States')
ax = plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos: f'${int(x/1000)}K'))
plt.xlim(0, 600000)
plt.show()
```


![Salary Distributions of Data Jobs in the US](3_Project\images\Salary_Distributions_in_the_US.png)

*Box plot visualizing the salary distributions for the top 6 Data Jobs title.*


#### Insights 

- Data Scientists Lead in Median Salary: Among the top 6 roles, Data Scientists tend to have the highest median salary, reflecting the demand for their expertise in advanced analytics, machine learning, and predictive modeling.

- Data Engineers Show High Earning Potential: Data Engineers have a wide salary range, with some outliers earning close to $600K annually. This highlights the value of their specialized skills in building and maintaining data infrastructure.

- Data Analysts Have a Lower Median Salary: Compared to Data Scientists and Data Engineers, Data Analysts generally have a lower median salary. This aligns with their focus on interpreting and visualizing data rather than developing complex models or infrastructure.


## 3. How well do jobs and skills pay for Data 
### Highest paid & Most demanded skills for Data Analysts

```python
fig, ax = plt.subplots(2, 1)

sns.set_theme(style="ticks")
sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, ax=ax[0], hue='median', palette='dark:b_r')

#df_DA_top_pay[::-1].plot(kind='barh', y='median', ax=ax[0], legend=False) 
#df_DA_top_pay.plot(kind='barh', y='median', ax=ax[0], legend=False)

ax[0].set_title('Top 10 Highest Paid Skills for Data Analysts')
ax[0].set_ylabel('')
ax[0].set_xlabel('')
ax[0].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))
ax[0].legend().remove()

sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, ax=ax[1], hue='median', palette='light:b')

#df_DA_skills[::-1].plot(kind='barh', y='median', ax=ax[1], legend=False)
#df_DA_skills.plot(kind='barh', y='median', ax=ax[1], legend=False)

ax[1].set_title('Top 10 Most In-Demand Skills for Data Analysts')
ax[1].set_ylabel('')
ax[1].set_xlabel('Median Salary (USD)')
ax[1].set_xlim(ax[0].get_xlim())  # Set the same x-axis limits as the first plot
ax[1].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))
ax[1].set_xlim(ax[0].get_xlim())
ax[1].legend().remove()

plt.tight_layout()
plt.show()
```
![the highest paid & Most in demand Skills for Data Analysts in the US](3_Project\images\top10_paying_skills.png)

*Two separate Bar graphs visualizing the highest paid skills and most in-demand skills for Data Analyst in the US.* 

### Insights 

- Highest Paid Skills: Advanced technical skills such as AWS, Spark, and Big Data command the highest median salaries for Data Analysts. These skills are often associated with more specialized and technical roles, reflecting their high value in the job market.

- Most In-Demand Skills: Foundational skills like SQL, Python, and Excel are the most in-demand for Data Analysts. These skills are versatile and widely applicable, making them essential for most data-related roles.

- Skill Gap Between Demand and Pay: While skills like SQL and Excel are highly in demand, they do not rank among the highest-paid skills. Conversely, specialized skills like AWS and Spark are less in demand but offer significantly higher salaries, indicating a premium for niche expertise.

### 4. What is the most optimal skill to learn for Data Analyst?

```python 
from adjustText import adjust_text
from matplotlib.ticker import PercentFormatter

#plt.scatter(df_DA_skills_high_demand['skill_percent'], df_DA_skills_high_demand['median_salary'])

sns.scatterplot(data=df_plot, x='skill_percent', y='median_salary', hue='Technology', s=100)

sns.despine()
sns.set_theme(style='ticks')

plt.xlabel('Percent of Data Analyst Jobs')
plt.ylabel('Median Salary ($USD)')  # Assuming this is the label you want for y-axis
plt.title('Most Optimal Skills for Data Analysts in the US')

# Get current axes, set limits, and format axes
ax = plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K'))  # Example formatting y-axis
ax.xaxis.set_major_formatter(PercentFormatter(decimals=0))  # Example formatting x-axis
# Add labels to points and collect them in a list
texts = []
for i, txt in enumerate(df_DA_skills_high_demand.index):
    texts.append(plt.text(df_DA_skills_high_demand['skill_percent'].iloc[i], df_DA_skills_high_demand['median_salary'].iloc[i], " " + txt))

# Adjust text to avoid overlap and add arrows
adjust_text(texts, arrowprops=dict(arrowstyle='->', color='gray'))

plt.show()
```
![Most optimal skill for Data Analysts in the US](3_Project\images\Most_optimal_skill_for_Data_Analyst.png)

*A scatter plot visualizing the most optimal skills ( high paying & high demand) for data analysts in the US*

### Insights:

- High-Paying Niche Skills: Skills like AWS, Spark, and Big Data are positioned in the high-salary range but have relatively lower demand. These skills are valuable for specialized roles and command a premium in the job market.

- Widely Applicable Skills: Foundational skills such as SQL and Python are both highly in demand and offer competitive salaries. These skills are essential for most data-related roles and provide a strong return on investment for learning.

- Skill Optimization: The scatter plot highlights a clear trade-off between demand and salary. While niche skills like AWS offer higher salaries, foundational skills like SQL and Python are more versatile and widely applicable, making them optimal for long-term career growth.


    
# What I Learned

Throughout this project, I gained valuable insights into the field of data analytics and honed my technical skills. Here are the key takeaways:

**Data Analysis and Visualization:** I learned how to manipulate and analyze datasets using Python libraries like Pandas and visualize trends effectively using Matplotlib and Seaborn.

**Market Trends:** By analyzing job postings and salary data, I understood the demand for specific skills in the data industry and how they correlate with earning potential.

**Skill Optimization:** I discovered the importance of balancing foundational skills like SQL and Python with niche technical skills like AWS and Spark to maximize career opportunities.

**Tool Proficiency:** I became proficient in using tools like Jupyter Notebook, AdjustText, and Matplotlib Ticker to enhance the quality of my analysis and visualizations.


# Final Insights


**SQL and Python Are Essential:** These foundational skills are highly in demand and widely applicable across data-related roles, making them indispensable for aspiring Data Analysts.

**Specialized Skills Command Higher Salaries:** Skills like AWS, Spark, and Big Data, while less in demand, offer significantly higher earning potential, highlighting the value of niche expertise.

**Skill Gap Between Demand and Pay:** There is a noticeable gap between the most in-demand skills and the highest-paying skills, emphasizing the need to strategically prioritize learning based on career goals.

**Visualization Matters:** Effective data visualization is crucial for uncovering actionable insights and communicating findings clearly, which is a key skill for any Data Analyst.



# Conclusion
This project has been an enriching journey into the world of data analytics. By analyzing job market trends and salary distributions, I gained a deeper understanding of the skills that are most valuable for Data Analysts. Foundational skills like SQL and Python remain critical for success, while specialized skills like AWS and Spark offer opportunities for higher earnings. The ability to analyze data, visualize trends, and draw actionable insights is not only a technical skill but also a strategic advantage in the competitive job market. This project has solidified my passion for data analytics and prepared me for the challenges and opportunities ahead in this exciting field.

