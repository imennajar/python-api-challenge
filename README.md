# python-api-challenge

In the previous project, we learned how to use matplotlib to include a statistics summary and to draw charts and plots for better reading and analysis📊. 
Now, we will see how to use IPAs to get a dynamic dataset and use our skills to analyze our data.
In this project, we will see  in a first part what is the weather like as we approach the equator, and in a second part how to plan future vacations using weather data skills.


## What we will learn from this project:

- How to generate the Cities List by Using the citipy Library
  
- How to use the OpenWeatherMap API to retrieve weather data from the cities list generated
  
- How Use the OpenWeatherMap API to retrieve weather data from the cities list generated in the started code
  
- How to use our skill to create Plots to Showcase the Relationship Between Weather Variables and Latitude: Latitude vs. Temperature, Latitude vs. Humidity, Latitude vs. Cloudiness, and Latitude vs. Wind Speed.
  
- How to use our skill to compute Linear Regression for Each Relationship: Latitude vs. Temperature in Northern and Southern Hemisphere, Latitude vs. Humidity in Northern and Southern Hemisphere,
  Latitude vs. Cloudinessin Northern and Southern Hemisphere, and Latitude vs. Wind Speed in Northern and Southern Hemisphere. We will include the linear regression line, the model's formula, and the rvalues
  
- How to create a map that displays a point for every city of our data using a weather caracteristique
  
- How to narrow down our data to find our ideal weather condition
  
- How to use the Geoapify API to find hotels (or any other accomodation)
  
- How to add the hotel name and the country as additional information in the hover message for each city in the map
  
## Instructions:

Prepare the data

retrieve weather data

Create Plots

Compute Linear Regression Plots

Create a maps

## Program:

### Tools:

- Pandas: it is a Python library for data manipulation and analysis

- Matplotlib.pyplot:  Matplotlib has a module named pyplot which makes things easy for plotting by providing features to control line styles, font properties, formatting axes etc. Matplotlib is a python library used to create 2D graphs and plots by using python scripts.

- Scipy.stats: it is a module that contains a large number of probability distributions.

- Jupyter Notebook: it is a web-based interactive computing platform that allows the user to compile all aspects of a data project.
  
  - Numpy: it is a Python library for working with arrays, in domain of linear algebra, fourier transform, and matrices.
  
- Requests: it is a module allowing to send HTTP requests using Python.

-  Hvplot: provides : it is a library in Python. It provides a high-level plotting API built on HoloViews that provides a general and consistent API for plotting data.
  
- OpenWeatherMap: it is an online service provides global weather data via API.
  
- Citipy

### Code to generate charts using pyplot methods
#### Bar Charts
```
# Generate a bar plot showing the total number of rows (Mouse ID/Timepoints) for each drug regimen using pyplot.

# prepare x axis and y_axis
x_axis = np.arange(len(mice_per_regimen ))
y_axis = mice_per_regimen['Mouse ID'] 
l=mice_per_regimen['Mouse ID'].max()
# create ticks 
x= mice_per_regimen.index.values
tick_location = [value for value in x_axis]
plt.xticks(tick_location, x,rotation="vertical") 
# creatte the plot
plt.bar(x_axis,y_axis, color='r', alpha=0.5,align = 'center')
# Set x and y limits
plt.xlim(-1, len(x_axis))
plt.ylim(0,l+10)
#Title 
plt.title("Total Measurements per Drug Regimen \n")
#labels
plt.xlabel('Drug Regimen \n')
plt.ylabel('#of Observed Mouse Timepoints \n')
```
plt.legend('Mouse ID', loc='upper right', frameon=True)
<img src='bar.png' style ='width:700px;height:300px'/>

#### Pie Chart
```
# Pie plot showing the distribution of female versus male mice using pyplot
mouse_gender = study_result_complete["Sex"].value_counts()
explode = (0.1,0)
colors =["blue", "pink"]
labels = mouse_gender.index
#create a pie chart 
plt.pie(mouse_gender, explode=explode, labels=labels, colors = colors,
        autopct="%1.1f%%", shadow=True, startangle=90) 

plt.title("distribution of female versus male mice")
plt.legend(labels, loc='upper right')
plt.axis("equal")
plt.ylabel('Sex')
```


<img src='pie.png' style ='width:700px;height:300px'/> 

#### Boxplots
```
# Box plot 
fig,ax = plt.subplots(figsize =(10, 7))
prop = dict(markerfacecolor='y', markersize=10,markeredgecolor='r')
ax.boxplot(tumor_vol_data,labels = treatments,flierprops=prop)
ax.set_title('Final tumor volume of each mouse across four of the treatment regimens\n')
ax.set_ylabel('Final Tumor Volume(mm3)\n')
ax.set_xlabel('\n Drug Regimen')
plt.show()
```
<img src='box.png' style ='width:700px;height:300px'/>

#### Line Plot
```
# Line plot of tumor volume vs. time point for a single mouse treated with Capomulin
capomulin_table = study_result_complete.loc[study_result_complete['Drug Regimen'] == 'Capomulin']
mousedata = capomulin_table.loc[capomulin_table['Mouse ID']== 'l509']
x_axix =mousedata['Timepoint']
y_axis = mousedata['Tumor Volume (mm3)']
plt.plot(mousedata['Timepoint'],mousedata['Tumor Volume (mm3)'],color='r', label='', marker = 'o')
plt.xlabel('Timepoint (days)')
plt.ylabel('Tumor Volume (mm3)')
plt.legend('Mouse l509',loc='lower right')
plt.title( 'Capomulin treatment of mouse l509')
plt.show()
```
<img src='lin1.png' style ='width:700px;height:300px'/>

#### Scatter Plots

```
# Scatter plot of mouse weight vs. the average observed tumor volume for the entire Capomulin regimen

capomulin_table = study_result_complete.loc[study_result_complete['Drug Regimen'] == "Capomulin"]


mice_group =capomulin_table.groupby(['Mouse ID']).mean()

av_tum =mice_group ['Tumor Volume (mm3)']

mouse_weight = mice_group['Weight (g)']

 #Create scatte rplot 
plt.scatter(mouse_weight, av_tum, marker='o', facecolors='blue', edgecolors='red',
              s=av_tum, alpha=0.75)
#title and labels
plt.title( 'mouse weight vs. average tumor volume: Capomulin regimen \n')
plt.xlabel('Weight (g)')
plt.ylabel(' Average Tumor volume (mm3)')
plt.savefig('scatter.png')
```
<img src='sca1.png' style ='width:700px;height:300px'/> 
<img src='sca2.png' style ='width:700px;height:300px'/>

## Tip:🪄

For a better analysis of the Capomulin results, generate lines plot of tumor volume vs. time point for more than one mouse treated.

<img src='lin1.png' style ='width:700px;height:300px'/>

<img src='lin3.png' style ='width:700px;height:300px'/> 

For a good comparison between Capomulin and Ramicane, generate a line plot of tumor volume vs. time point for two mice treated wuth the two different drug regimens
<img src='lin2.png' style ='width:700px;height:300px'/> 

