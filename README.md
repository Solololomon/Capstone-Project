# Data Engineering Capstone Project for Xander Talent
## Solomon Williams - 8th November 2022

### Repository Contents
This repository contains:<br>
- Two Jupyter notebooks in which all of my Python code is held. Throughout each notebook, I have documented each step, and have included the project objectives and  my conclusions. These outcomes will be included in this README file.
- Several .csv files; the initial set of test data, and the rest that have been generated either in my notebook, or by creating a view in MySQL. All SQL queries have been included in the Jupyter notebooks where the views have been imported.
- Five .png files; a final figure/plot relating to each objective (outlined below).
- A .docx file explaining the project requirements.
- This README file.

### Introduction
For this project, I have been asked to produce insights into various aspects of a fictional company that sells a number of products. The insights will be derived from a sample data set, and should be targeted towards stake holders, aiming to outline:

1 - Product performance <br>
2 - User Demographics <br>
3 - Whether sales are seasonal or consistent throughout the year <br>
4 - Whether the company's marketing spend across various UK regions can be justified <br>
5 - The average CPA (Cost per acquisition) of each region, and how it compares to the expected value. <br>

Full information on the project requirements is available in the 'Project Requirements.docx' file.

The sample data set is given in .csv form, and I have been provided with a MySQL database in which I can generate tables/views to use in the project. The project will be conducted in two distinct phases: data cleaning, and visualisation.

### Phase 1: Data Cleaning
#### See notebook: 'Capstone_1_Data_Cleaning.ipynb'
As the raw sample data has been manually gathered, the first phase of this project is data cleaning. This includes removing negative numbers and null values, and splitting the date entries by year and month. As there are no entries for the region 'UK South' (despite being mentioned in the project brief), I will, from this point forward, assume this to be intentional and that this region has simply recorded no orders.

This phase ends with a clean Pandas DataFrame that is saved as a .csv and (manually) translated into a MySQL table.

### Phase 2: Visualisation
#### See notebook: 'Capstone_2_Visualisation.ipynb'
With a cleaned set of data imported as a Pandas DataFrame, I will now go through each objective methodically using the relevant MySQL view, or otherwise, as necessary. Each objective section ends with a plot, saved as a .png file, and a conclusion. I will briefly outline here the methodology in achieving each objective, as well as the conclusion drawn.

### Objective 1: Product Performances
#### See figure: 'Product_Sales.png'
I have deconstructed the original DataFrame to produce a small table of each product and total quantity sold. I have done this using python, but have also included how this could have been done in MySQL. Using this information, I have decided to convey the data in a bar chart.
#### Conclusion:
From this plot it's clear to see that toothbrushes are performing better than toys, serving as roughly 60% of all purchases.

### Objective 2: Demographic Information 
#### See figure: 'Demographics.png'
I have generated a view in MySQL that splits the data into various age ranges, with the value counts representing the number of customers in each age range (ignoring quantity of products bought). I have also recorded value counts for customers across each region. I have opted to convey this information in the form of two pie charts representing age and region demographics, respectively, as percentages.
#### Conclusion:
The first of these visuals shows that the most popular age demographic is people under 25, followed by those over 55 and then between 30-34. Conversely, the least popular age demographics are ages 25-29 and 40-44, for which there were no recorded sales, and people aged 45-54, who comprised only 8% of customers.

The second visual shows that the North East and South East are by far the most popular customer regions. Conversely, UK North represents around just 16% of customers, and the South recorded none whatsoever.

Marketing may want to either focus on their best-performing demographics, or help boost the under-performing ones. Either way, these visuals should help them draw the conclusions they need and allocate resources, as necessary.

### Objective 3: Sales Throughout the Year 
#### See figure: 'Month_Sales.png'
Again, using a MySQL view, I have counted the quantity of products sold for each month. I have decided it best to convey this information in the form of a standard line plot, making it easier to identify trends and determine whether or not sales are consistent throughout the year.
#### Conclusion:
It's clear that sales perform considerably worse around May than at any other time of year. This is an indication that sales are indeed seasonal, drastically underperforming in the summer months. Conversely, they perform best between January and March, with the peak number of sales occurring in the spring. After summer, the sales increase again during autumn, but then there is another clear downward trend as winter begins. We could expect to see that the sales would pick up again in the new year, completing the cycle.

### Objective 4: Performance By Region
#### See figure: 'Region_Sales.png'
Generating two MySQL views, I have separated each region by both total sales, and by sales of individual products. I have plotted these side by side as two bar charts that convey sales information across the different regions.
#### Conclusion:
Firstly, marketing in the UK South region has proven to be wasteful expenditure, as there have been no recorded sales. Undoubtedly, the expenditure can be justified in the South East as they have recorded 54.5% of all sales with just 44% of total customers. The North East represents 40% of customers, yet they only made up 30.3% of total sales, suggesting that people in this region purchase products in lower quantities. Finally, while, on the face of it, it seems that the North is lacking, with 15.2% of total sales from just 16% of customers, this region is actually performing fairly well.

Outside of the South East, there were no recorded toys sales. If the marketing team have been advertising toys outside of this region, it's safe to say that this was wasteful expenditure. Moreover, despite this high volume of toy sales, the toothbrush sales in the South East were fairly low, comparable to those in the North (despite a large difference in customer numbers), and the majority being sold in the North East. This could still be indicative of wasteful expenditure if the allocation of marketing spend was uniform across all regions, as we'd hope to see an equal split in customer numbers and sales across each region if that were the case.

### Objective 5: CPAs Per Region
#### See figure: 'Region_CPAs.png'
The given expected CPA values are available at a web address, and so I have decided to use Requests and BeautifulSoup to web scrape this information into a dictionary with region as the key and CPA as the value. As these values seem to pertain to sales in October 2021, I had to filter the dataset to obtain only the relevant information, which was done using another MySQL view. I have zipped this information into a single DataFrame detailing the actual and expected CPA averages for each region, which will then be plotted into a stacked bar chart. 
#### Conclusion:
For all three regions where we had data, it was evident that the actual CPA was significantly below the expected value. Surprisingly, UK north had the highest actual CPA despite having a lower expected CPA than the others. Nonetheless, this is a positive finding, and shows that the current marketing strategies are acquiring customers at a lower cost than anticipated.

### Recommendations for Future Projects
Going forward, this project could be refined by using the pymysql package, and implementing pymysql.connect() to avoiding manually interacting with the database and exporting csv files to be read into the notebook. If the database was to be scaled up to a much larger size, this would undoubtedly be a more efficient way of pushing and pulling data to and from it. Aside from this, the current model has decent scalability and fault tolerance, providing entries are of the expected type. It could be worthwhile adding basic tests for the input data to ensure that it will be compatible with the model.
