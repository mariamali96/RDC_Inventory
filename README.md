# RDC_Inventory
import numpy as np 
import pandas as pd

# Data visualization modules of small data set
import matplotlib.pyplot as plt

import seaborn as sns
sns.set_style('darkgrid') # setting the style of the plots

pd.options.display.max_columns = 999 
pd.options.display.max_rows = 999 

from subprocess import check_output

data = pd.read_csv('metro_last_month.csv')

#PARSING

#data['Date'] = pd.to_datetime(data['Date'])
#plot ZHVI Per Sqft vs date
df= pd.DataFrame(data)
#correlation between avg listing price and number of days on market
#try answer the question does longer or shorter days mean higher avg 
data.groupby(data['Avg Listing Price'])['Days on Market'].mean().dropna().plot(linewidth=4, figsize=(15, 6))

plt.title('avg price vs days on market', fontsize=14)
plt.ylabel('Price\n')
plt.show()
#Avg price & pending ratio of the market, does it affect the price if the ratio is high or low?
data.groupby(data['Avg Listing Price'])['Pending Ratio'].mean().dropna().plot(linewidth=4, figsize=(15, 6))
plt.title('avg price vs days on market', fontsize=14)
plt.ylabel('Price\n')
plt.show()


####################################################################################################################
#Invetory history data set of United sates 2012-2018

data = pd.read_csv('US_Hist.csv')

#PARSING

data['Month'] = pd.to_datetime(data['Month'])
data['Year'] = data['Month'].apply(lambda x: x.year)
data['month'] = data['Month'].apply(lambda x: x.month)

# testing the hypothesis that the listing price steadly increasing yearly

data.groupby(data['Year'])['Avg Listing Price'].mean().dropna().plot(linewidth=4, figsize=(15, 6))

plt.title('Avg Listing Price yearly', fontsize=14)
plt.ylabel('Price\n')
plt.show()

# Testing which month over the years is the hot month of pricing
data.groupby(data['month'])['Avg Listing Price'].mean().dropna().plot(linewidth=4, figsize=(15, 6))

plt.title('Hot Month?', fontsize=14)
plt.ylabel('Price\n')
plt.show()
