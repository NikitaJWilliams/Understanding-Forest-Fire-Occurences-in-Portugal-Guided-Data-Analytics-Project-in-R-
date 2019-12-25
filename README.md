# Understanding Forest Fire Occurrences in Portugal (Data Visualization Project)

## Introduction 
According to Cortez and Morais, forest fires inflict major harm on the environment and economy. One way to minimize the economic and ecological damage caused by forest fires is to predict their occurrence. In this project, I apply various graphical tools in R to identify days of the week and months of the year which experience the greatest number of forest fires. Lastly, I test a common assumption that the forest fire area serves as a good measure of forest fire severity. The dataset that I use contains a sample of forest fires in Portugal. Cortez and Morais state that the natural phenomenon greatly affects the country. 
## Variables
| Variable | Description  |
| :---: | :---: |
| X | X-axis spatial coordinate within the Montesinho park map: 1 to 9 |
| Y | Y-axis spatial coordinate within the Montesinho park map: 2 to 9 |
| month | month of the year: 'jan' to 'dec' |
| day | day of the week: 'mon' to 'sun' |
| FFMC | Fine Fuel Moisture Code index from the FWI system: 18.7 to 96.20 |
| DMC | Duff Moisture Code index from the FWI system: 1.1 to 291.3 |
| DC | Drought Code index from the FWI system: 7.9 to 860.6 |
| ISI | Initial Spread Index from the FWI system: 0.0 to 56.10 |
| temp | Temperature in Celsius degrees: 2.2 to 33.30 |
| RH | Relative humidity in percentage: 15.0 to 100 |
| wind | Wind speed in km/h: 0.40 to 9.40 |
| rain | Outside rain in mm/m2 : 0.0 to 6.4 |
| area | The burned area of the forest (in ha): 0.00 to 1090.84 |

You can learn more about the variables used in this dataset at [Natural Resources Canada](http://cwfis.cfs.nrcan.gc.ca/background/summary/fwi).
## Data Analysis
To determine when forest fires occur the most in Portugal, I plotted two seperate bar charts: the first bar chart depicts frequency of forest fires for each month and the second bar chart demonstrates frequency of forest fires for each day of the week. 

![](https://i.ibb.co/g9dyVNW/Month-Bar-Chart.png)
![](https://i.ibb.co/85bfHyf/Day-Bar-Chart.png)

In the case of Portugal, August and September are by far the most popular months when it comes to forest fire incidents. On the other hand forest fires happen more on weekends than they do on weekdays with the exception of Friday. The distribution of the number of forest fires has a larger spread across different months than it does across different days of the week which is arguably not surprising.

To determine potential causes of the temporal variation in the number of forest fires across different days and months, I made a series of boxplots to picture the distribution variables that relate to forest fires over time. If these variables fluctuate as time moves forward, then they may help us anticipate forest fires with a greater degree of accuracy. 

### Day of the Week
![](https://i.ibb.co/WkPQtjC/Boxplot-Daily.png)

According to the above boxplots, the variables that relate to forest fires do not vary as the days of the week change. Despite the presence of a few outliers for each dependent variable, the median and the size of the boxes are of roughly the same size across different days of the week.  
### Month
![](https://i.ibb.co/zxL16wf/Boxplot-Monthly.png)

The second class of boxplots tells a different story when *month* represents time: the distribution of variables, which display connection with forest fires, alter with time! Unlike in the first group of boxplots, the median and the size of the boxes differ substantially for each month; however, *rain* is an exception to this transformation. That being said *temp* and *DC* can explain the abnormal high frequency of forest fires in August and September in Portgual as these measures tend to be relatively steep towards the end of the summer. 

Right now I would like to turn attention to measuring the intensity of forest fires. A popular assumption in the forest fire research is that *area* serves as a good indicator for severity of the fire. The intuition behind the assumption is that a major forest fire will cause damage over a larger land area. To test the validity of this argument, I made a scatter plot of *area* where *area* is the dependent variable and factors that relate to forest fires are independent variables.
### Scatter Plot of Area
![](https://i.ibb.co/9hMj4kZ/Scatter-Area.png) 

According to the scatter plots, there is no clear relationship between the *area* and the independent variables. Perhaps the only meaningful observation to infer from the graphs is that *area* values are mostly clustered around 0. 

To visualize the distribution of *area*, I plotted a histogram.

![](https://i.ibb.co/bs8L6k0/Histogram-of-Area.png) 

The histogram demonstrates that *area* ranges approximately from 0 to approximately 100. There is a small subset of values that exceeds 100, but given the number of observations in the dataset, it is not large enough to make a substantial difference.

Given this piece of information, I modified the original set of scatter plots where the values of *area* are restricted from 0 to 100. 

### Scatter Plot of Area (0 to 100)

![](https://i.ibb.co/wCwgCwk/Scatter-Plot-Area-0-to-100.png)

The new scatter plots show that when we impose an upper bound limit of 100 on *area*, the general patter does not change: *area* values are centered around 0. Thus, there is no clear relationship between *area* and severity of the forest fires in Portugal.

## Code

To graph multiple boxplots, I created my own *create_boxplot* function. 
```
create_boxplot <- function(x,y) {
  ggplot(data = forest_fires) + 
  aes_string(x = x, y = y) + 
  theme(panel.background = element_rect(fill = "white")) + 
  geom_boxplot()
}
```
To graph multiple scatter plots, I created my own *created_scatter* function. 
```
create_scatter <- function (x,y)    {
   ggplot(data = forest_fires) + 
   aes_string(x = x, y = y) +
   theme(panel.background = element_rect(fill = "white")) + 
   geom_point(alpha = 0.3)
}
```
To view the rest of my code, you can access the *R Script* file.
## Conclusion
My sample results show that forest fires are most likely to occur during the months of August and September in Portgual. High temperatures and dry conditions can explain as to why this is the case. While many people may believe that *area* is a good measure of forest fire intensity, I challenge its legitimacy using scatter plots. 

## References
Cortez and Morais, *A Data Mining Approach to Predict Forest Fires using Meteorological Data*. [Link to research paper](http://www3.dsi.uminho.pt/pcortez/fires.pdf)

The dataset is extracted from [UC Irvine Machine Learning Repository](https://archive.ics.uci.edu/ml/machine-learning-databases/forest-fires/)

