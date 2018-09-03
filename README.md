
### <center>**Data Analysis of Premier League**</center>

##### This is a jupyter notebook which analyzes the data and gives meaningful insights from the premier league table since it's inception on 1992, upto 2018. The new season is not added as the current league is going on (2018/2019).  The data is scraped from workfootball.net. Only the premier league table is scrapped and the data is analyzed. Minimal libraries are used to analyze the data.


```python
import os
import sys
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from matplotlib.pyplot import figure

%matplotlib inline
```


```python
# # # Given
start_season_year = 1992
end_season_year = 2018
total_seasons = 26   # # (1992-2018)
total_teams = 20
relegation_count = 3
relegation_threshold = 18
column_headers = ['Teams', 'M', 'W', 'D', 'L', 'Goals', 'Diff', 'Pts']
```


```python
data_dictionary = {}
for i in range(total_seasons):
    season_date = i + start_season_year
    data_dictionary[season_date] = pd.read_csv('../data/https___www.worldfootball.net_ ({0}).csv'.format(i), header=None, index_col=0)
    
    individual_dataframe = data_dictionary[season_date]
    
    # # Remove unknown columns
    del individual_dataframe[9]
    del individual_dataframe[10]
    
    # # Remove unknown index
    individual_dataframe.drop(individual_dataframe.index[:2], inplace=True)
    
    # # Good Columns Names
    individual_dataframe.columns = column_headers
    
    individual_dataframe = individual_dataframe.rename_axis(None, inplace=True)
```

### <center>**Premier League Table 2003/2004**</center>


```python
data_dictionary[2003]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Teams</th>
      <th>M</th>
      <th>W</th>
      <th>D</th>
      <th>L</th>
      <th>Goals</th>
      <th>Diff</th>
      <th>Pts</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Arsenal FC</td>
      <td>38</td>
      <td>26</td>
      <td>12</td>
      <td>0</td>
      <td>73:26</td>
      <td>47</td>
      <td>90</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chelsea FC</td>
      <td>38</td>
      <td>24</td>
      <td>7</td>
      <td>7</td>
      <td>67:30</td>
      <td>37</td>
      <td>79</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Manchester United</td>
      <td>38</td>
      <td>23</td>
      <td>6</td>
      <td>9</td>
      <td>64:35</td>
      <td>29</td>
      <td>75</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Liverpool FC</td>
      <td>38</td>
      <td>16</td>
      <td>12</td>
      <td>10</td>
      <td>55:37</td>
      <td>18</td>
      <td>60</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Newcastle United</td>
      <td>38</td>
      <td>13</td>
      <td>17</td>
      <td>8</td>
      <td>52:40</td>
      <td>12</td>
      <td>56</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Aston Villa</td>
      <td>38</td>
      <td>15</td>
      <td>11</td>
      <td>12</td>
      <td>48:44</td>
      <td>4</td>
      <td>56</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Charlton Athletic</td>
      <td>38</td>
      <td>14</td>
      <td>11</td>
      <td>13</td>
      <td>51:51</td>
      <td>0</td>
      <td>53</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Bolton Wanderers</td>
      <td>38</td>
      <td>14</td>
      <td>11</td>
      <td>13</td>
      <td>48:56</td>
      <td>-8</td>
      <td>53</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Fulham FC</td>
      <td>38</td>
      <td>14</td>
      <td>10</td>
      <td>14</td>
      <td>52:46</td>
      <td>6</td>
      <td>52</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Birmingham City</td>
      <td>38</td>
      <td>12</td>
      <td>14</td>
      <td>12</td>
      <td>43:48</td>
      <td>-5</td>
      <td>50</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Middlesbrough FC</td>
      <td>38</td>
      <td>13</td>
      <td>9</td>
      <td>16</td>
      <td>44:52</td>
      <td>-8</td>
      <td>48</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Southampton FC</td>
      <td>38</td>
      <td>12</td>
      <td>11</td>
      <td>15</td>
      <td>44:45</td>
      <td>-1</td>
      <td>47</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Portsmouth FC</td>
      <td>38</td>
      <td>12</td>
      <td>9</td>
      <td>17</td>
      <td>47:54</td>
      <td>-7</td>
      <td>45</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Tottenham Hotspur</td>
      <td>38</td>
      <td>13</td>
      <td>6</td>
      <td>19</td>
      <td>47:57</td>
      <td>-10</td>
      <td>45</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Blackburn Rovers</td>
      <td>38</td>
      <td>12</td>
      <td>8</td>
      <td>18</td>
      <td>51:59</td>
      <td>-8</td>
      <td>44</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Manchester City</td>
      <td>38</td>
      <td>9</td>
      <td>14</td>
      <td>15</td>
      <td>55:54</td>
      <td>1</td>
      <td>41</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Everton FC</td>
      <td>38</td>
      <td>9</td>
      <td>12</td>
      <td>17</td>
      <td>45:57</td>
      <td>-12</td>
      <td>39</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Leicester City</td>
      <td>38</td>
      <td>6</td>
      <td>15</td>
      <td>17</td>
      <td>48:65</td>
      <td>-17</td>
      <td>33</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Leeds United</td>
      <td>38</td>
      <td>8</td>
      <td>9</td>
      <td>21</td>
      <td>40:79</td>
      <td>-39</td>
      <td>33</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Wolverhampton Wanderers</td>
      <td>38</td>
      <td>7</td>
      <td>12</td>
      <td>19</td>
      <td>38:77</td>
      <td>-39</td>
      <td>33</td>
    </tr>
  </tbody>
</table>
</div>



### <center>**Search for the most successful club's in England**<center/>


```python
# # # Creating a Winner's dictionary with clubs and their respective title winning years
winners_dict = {}
winners_hist = {}
for i in range(total_seasons):
    season_date = i + start_season_year
    winner_club = data_dictionary[season_date].loc['1'][0]
    winners_dict[season_date] = winner_club
    
    # # For Winners Histogram
    if winner_club in winners_hist:
        winners_hist[winner_club] += 1
    else:
        winners_hist[winner_club] = 1
```


```python
winners_hist
```




    {'Manchester United': 13,
     'Blackburn Rovers': 1,
     'Arsenal FC': 3,
     'Chelsea FC': 5,
     'Manchester City': 3,
     'Leicester City': 1}




```python
winners_dict
```




    {1992: 'Manchester United',
     1993: 'Manchester United',
     1994: 'Blackburn Rovers',
     1995: 'Manchester United',
     1996: 'Manchester United',
     1997: 'Arsenal FC',
     1998: 'Manchester United',
     1999: 'Manchester United',
     2000: 'Manchester United',
     2001: 'Arsenal FC',
     2002: 'Manchester United',
     2003: 'Arsenal FC',
     2004: 'Chelsea FC',
     2005: 'Chelsea FC',
     2006: 'Manchester United',
     2007: 'Manchester United',
     2008: 'Manchester United',
     2009: 'Chelsea FC',
     2010: 'Manchester United',
     2011: 'Manchester City',
     2012: 'Manchester United',
     2013: 'Manchester City',
     2014: 'Chelsea FC',
     2015: 'Leicester City',
     2016: 'Chelsea FC',
     2017: 'Manchester City'}




```python
width = 0.5
figure(num=None, figsize=(16, 6), dpi=80, facecolor='w', edgecolor='k')

y_ticks = np.arange(0, 15)
plt.yticks(y_ticks)

plt.bar(winners_hist.keys(), winners_hist.values(), width, color='green')
```




    <BarContainer object of 6 artists>




![png](output_11_1.png)


##### <center>This figure shows that the most successful club in the modern era of premier league is Manchester United</center>

### <center>**Search for the most season with a close difference**</center>

##### <center>Calculating the seasons with the difference in points between the highest placed team and the lowest placed team. This stats will show the competitiveness between the teams from top to bottom. This closer the difference, the more chance for each and every club, more the entertaining season.</center>


```python
# # Getting the difference in points season
difference_hist = {}
difference_points = []
for i in range(total_seasons):
    season_date = i + start_season_year

    winner_point = data_dictionary[season_date].loc['1'][7]
    loser_point = data_dictionary[season_date].loc['20'][7]
    
    difference_points.append(int(winner_point) - int(loser_point))
    difference_hist[season_date] = (int(winner_point), int(loser_point))
```


```python
figure(num=None, figsize=(15, 6), dpi=80, facecolor='w', edgecolor='k')
x = list(difference_hist.values())
data = list(difference_hist.keys())

plt.boxplot(x=x, data=data, labels=data, showmeans=True)
plt.show()
```


![png](output_16_0.png)


##### <center>This figure shows the box plots of the points obtained in the premier league</center>

##### From this box plot we can find that
- *2007 has the least number of points obtained*
- *2017 has the highest number of points obtained*
- *1992 had the lowest difference between the highest point scoring club and lowest point scoring club*
- *2005 has the largest difference between the highest point scoring club and lowest point scoring club*
- *More Stats can be extracted from this box plot*

### <center>**Getting the best place of each and every club**</center>


```python
best_place_dict = {}
best_place_date_dict = {}
for i in range(total_seasons):
    season_date = i + start_season_year
    for j in range(total_teams):
        team_name = data_dictionary[season_date].loc[str(j+1)][0]
        # # Check whether the team is already in the dictionary
        if team_name in best_place_dict:
            # # Compare the best place from the old place
            if best_place_dict[team_name] > j+1:
                best_place_dict[team_name] = j+1
        else:
            best_place_dict[team_name] = j+1
            best_place_date_dict[team_name] = season_date
```


```python
figure(num=None, figsize=(15, 25), dpi=80, facecolor='w', edgecolor='k')
plt.xlabel('Best Place Finish')
plt.ylabel('Clubs')

x_ticks = np.arange(1, 21)

plt.grid(axis='both')
plt.xticks(x_ticks)
plt.scatter(x=best_place_dict.values(), y=best_place_dict.keys())
```




    <matplotlib.collections.PathCollection at 0x7f999b353dd8>




![png](output_21_1.png)


##### <center>This figure shows the scatter plot of the clubs with their best place finish in the premier league</center>

##### From this scatter plot we can find that
- *There are only 6 clubs who have won the premier league*
- *There are no clubs whose best place finish is the 12th place*
- *Cardiff is the only club who has never had a best place finish above 20th place*
- *There are only 48 teams who have competed in the premier league on the span of 26 years*
- *Blackburn Rovers are the only team to won the premier league and relegated*

### <center>**Getting the teams that has never been relegated after entry to the premier league**</center>


```python
for i in range(total_seasons):
    season_date = i + start_season_year
    for j in range(relegation_count):
        team_name = data_dictionary[season_date].loc[str(relegation_threshold + j)][0]
        if team_name in best_place_date_dict:
            del best_place_date_dict[team_name]
```


```python
figure(num=None, figsize=(26, 15), dpi=80, facecolor='w', edgecolor='k')
plt.xlabel('Inception Year')
plt.ylabel('Clubs')

x_tick = np.arange(1992, 2018, 1)

plt.grid(axis='both')
plt.xticks(x_tick)
plt.scatter(x=best_place_date_dict.values(), y=best_place_date_dict.keys())
```




    <matplotlib.collections.PathCollection at 0x7f999b377390>




![png](output_26_1.png)


##### <center>This figure shows the scatter plot of the clubs with their top flight stay and never relegated</center>

##### From this scatter plot we can find that
- *There are only 6 clubs who stayed on the top flight and never relegated*
- *3 clubs have stayed on the top flight and aren't related upto now*

### <center>**Getting the maximum number of wins from the teams**</center>


```python
total_wins_dict = {}
for i in range(total_seasons):
    season_date = i + start_season_year
    for j in range(total_teams):
        team_name = data_dictionary[season_date].loc[str(j+1)][0]
        wins = data_dictionary[season_date].loc[str(j+1)][2]
        if team_name in total_wins_dict:
            total_wins_dict[team_name] += int(wins)
        else:           
            total_wins_dict[team_name] = int(wins)
```


```python
figure(num=None, figsize=(15, 25), dpi=80, facecolor='w', edgecolor='k')
plt.xlabel('Number of Wins')
plt.ylabel('Clubs')

x_ticks = np.arange(5, 630, 30)

plt.grid(axis='both')
plt.xticks(x_ticks)
plt.scatter(x=total_wins_dict.values(), y=total_wins_dict.keys())
```




    <matplotlib.collections.PathCollection at 0x7f999b5fdba8>




![png](output_31_1.png)


##### <center>This figure shows the scatter plot of the clubs with their wins</center>

##### From this box plot we can find that
- *Manchester United has the most wins spanning 600+ wins on their top flight stay*
- *Arsenal and Chelsea are 2nd and 3rd place with 520+ wins*

##### This is my first crack on data analysis. Hope you like it :). More analysis can be done from this raw data so contributions are always welcomed:). If there are any bugs, they are always welcomed!!

##### Notebook Created by: [Sulabh Shrestha](https://github.com/codexponent/)
###### - Connect with me on [Linkedin](https://www.linkedin.com/in/sulabhshrestha/) & [Twitter](http://www.twitter.com/codexponent)
