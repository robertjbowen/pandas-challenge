# pandas-challenge

This project was to manipulate Pandas Data Frames using Jupyter Notebook to analyze the purchasing data from a fantasy game called Heroes of Pymoli. The game is a free to play online, but encourages players to purchase online items to enhance their playing experience.


### Documents in this repository are:

HeroesOfPymoli.ipynb - My Jupyter Notebook file running a Python 3 kernel that contains all of the code for conducting the data analysis 

ObservableTrends.txt - Text file containing three observed trends from the data analysis

Resources directory containing the source file of purchasing data - purchase_data.csv

Checkpoints directory containing checkpoint .ipynb files


### Design concept:

The project begins with downloading a set of purchase and player data into a data frame (purchase_data). Because players have the ability to make multiple purchases, in order to analyze based on players, it was necessary to create a copy of the original data set and remove duplicate instances of players who made multiple purchases (player_data). This copy makes it possible to work with the reduced data set while still preserving the original data for other analysis. This was completed once at the beginning and called as required through out the analysis.

Each subsequent step in the analysis created a new Data Frame from either the original data set (purchase_data) or the scubbed data set (player_data) depending on the specific analysis to be conducted.

***
### Analysis Observations:

*1) Males make up the vast majority (84%) of all players outnumbering Females 6 to 1. But females players spend on average almost 10% more than male players.*

*2) 3/4s of all Players fall into the 15-29 year old (high school and college) age range and account for 76% of total revenue.*

*3) The most popular items are also the most profitable. The most popular items are also priced higher than average suggesting players are willing to pay more for items they want. There aren't any big sellers. Out of 780 sales, the most sales of a single item is only 13 (1.6%). Most players only buy one item.*

***
### Analysis Steps:

#### Player Count

The first step in the analysis was to determine the player count. This could be done in two ways. 1) by finding the length of a list of the unique values in the 'SN' column of the purchase_data data frame. As I did.  or 2) finding the length of the reduced data frame player_data. Each return a value of 576. This value was read into a data frame called total_players and displayed.

![alt tag]
(

#### Purchasing Analysis (Total)

This step involved creating a new data frame and reading into it 4 calulated values from the purchase_data data frame. 

1) The number of unique items was determined the same as above, by finding the length of a list of the unique values in the 'Item Name' column. 
2) Average Price was determined by calculating the mean of the 'Price' column. 
3) Number of purchases was determined by counting the number of values in the Purchase ID column. 
4) Total Revenue was determined by summing the 'Price' column.

The price calulations were stored in the list as float values without dollar signs and with extra decimal places. Rather than changing the data in the table by mapping formatting to the columns, I applyed style formatting to the data when it was displayed to have the currency values display properly.


#### Gender Demographics

This is the first step in the analysis to rely on the player_data dataframe in order to determine the correct numbers of male and female players. This involved creating a new dataframe (gen_out) by calculating the value counts of the 'Gender' column from the player_data data frame. This column was then renamed to 'Total Count' and another column 'Percentage of Players' was calulated by dividing each of the values in the 'Total Count' column by the value calculated in the  Player Count analysis above. This give sthe total number of players grouped by gender and their overall percentage of the total players. The output was also styled to display the percentages properly marked and with two decimal places.


#### Purchasing Analysis (Gender)

This involved creating a new dataframe (puchase_gen) by copying the 'Gender' and 3 copies of the 'Price' column from the purchase_data data frame. These columns were renamed to 'Gender','Purchase Count','Average Purchase Price', and 'Total Purchase Value'. I then used the groupby().agg() method to group the data in the data frame based on gender and applied differnet functions to each column. 

1) 'Purchase Count' counted the total values for each gender. 
2) 'Average Purchase Price' determined the mean price payed for each gender.
3) 'Total Purchase Value' calculated the sum of the price of all purchases for each gender.

The 'Average Total Purchase Per Person' was calculated and appended to the data frame by dividing each row of the 'Total Purchase Value' column by the total number of players determined above. Again the output was styled to display currency values properly.


#### Age Demographics

Age demographis were determined by creating a black dataframe (age_data) and using a pd.cut() method to read in the data from the 'Age' colun of the player_data data frame and divide it into groups starting at under age 10, then every 4 years to age 39, and then all 40 and over. The value counts of each of these bins were then read into another data frame (age_out) and the column was renamed 'Total Count'. A new column was appended to the data frame which calculated the 'Percentage of Players' for each age by dividing each row of the 'Total Count' column by the total number of players from above. The 'Percentage of Players' was formatted to display percentages properly. The output age bins were displaying out of order so I sorted the data frame by the index prior to display.  


#### Purchase Analysis (Age)

This step in the analysis combined techniques employed earlier in the anlysis. A new dataframe (puchase_age) was created by copying the 'Age' and 3 copies of the 'Price' column from the purchase_data data frame. The columns were renamed and then binned the same as the Age Demographics above. The columns were then grouped b the age ranges,, the 'Average Total Purchase Per Person' was calculated and appended to the data frame and the output was style formatteed to display currency correctly.


#### Top Spenders

Similar to Purchasing Analysis (Gender) above. This analysis used the 'SN' column of data rather than the 'Gender' column. The data frame columns were renamed and then grouped by the 'SN' column using the groupby().agg() method to allow each column to be grouped using a different format. The data frame was then sorted from largest to smallest using the 'Total Purchadse Value' column and the currency display formats were mapped to the columns for display.


#### Most Popular Items

Similar to Top Spenders above.The data frame was created, renamed, grouped and sorted. Inorder to retain the integrity of the data for follow on analysis, the currency formatting was applied to the output command rather than mapped to the columns directly.

#### Most Profitable Items

The most simple step of the analysis. Because I did not map the formatting directly to the previous data frame, I was able to simply sort the data by the 'Total Purchase value' column from largest to smallest and apply the style format to the output as above.
