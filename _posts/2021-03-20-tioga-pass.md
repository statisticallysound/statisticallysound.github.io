---
layout: post
title: Tioga Pass Opening Date
---

Every winter, Tioga Pass in Yosemite National Park closes due to the snow and the unsafe driving conditions. Depending on the snowfall for the year and the road conditions, Tioga Pass opens between May and June. Tioga Pass usually opens to bikes only for a week, and then it opens to the general public afterwards. What's a reasonable prediction for the 2021 Tioga Pass Opening Date?

# Cleaning the Data

First, let's import the historical opening dates from the [NPS](https://www.nps.gov/yose/planyourvisit/seasonal.htm). The National Park Service (NPS) has recorded the historical opening dates for Tioga Pass since the 1980s.


```python
import pandas as pd
import numpy as np

df = pd.read_csv('.../yose-Websitesortabledataelementsheetsroadscampgroundstrails.csv')
df
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
      <th>Year</th>
      <th>Tioga Opened</th>
      <th>Tioga Closed</th>
      <th>Glacier Pt Opened</th>
      <th>Glacier Pt Closed</th>
      <th>Mariposa Grove Opened</th>
      <th>Mariposa Grove Closed</th>
      <th>Snowpack as of Apr 1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020 *</td>
      <td>15-Jun</td>
      <td>5-Nov</td>
      <td>11-Jun</td>
      <td>5-Nov</td>
      <td>11-Jun</td>
      <td>25-Dec</td>
      <td>46%</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2019 *</td>
      <td>1-Jul</td>
      <td>19-Nov</td>
      <td>10-May</td>
      <td>25-Nov</td>
      <td>16-Apr</td>
      <td>26-Nov</td>
      <td>176%</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018 *</td>
      <td>21-May</td>
      <td>20-Nov</td>
      <td>28-Apr</td>
      <td>20-Nov</td>
      <td>15-Jun</td>
      <td>30-Nov</td>
      <td>67%</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017 *</td>
      <td>29-Jun</td>
      <td>14-Nov</td>
      <td>11-May</td>
      <td>14-Nov</td>
      <td>Closed</td>
      <td>Closed</td>
      <td>177%</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016 *</td>
      <td>18-May</td>
      <td>16-Nov</td>
      <td>19-Apr</td>
      <td>16-Nov</td>
      <td>Closed</td>
      <td>Closed</td>
      <td>89%</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015 *</td>
      <td>4-May</td>
      <td>1-Nov</td>
      <td>28-Mar</td>
      <td>2-Nov</td>
      <td>No closure</td>
      <td>6-Jul</td>
      <td>7%</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2014 *</td>
      <td>2-May</td>
      <td>13-Nov</td>
      <td>14-Apr</td>
      <td>28-Nov</td>
      <td>No closure</td>
      <td>No closure</td>
      <td>33%</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2013</td>
      <td>11-May</td>
      <td>18-Nov</td>
      <td>3-May</td>
      <td>18-Nov</td>
      <td>No closure</td>
      <td>No closure</td>
      <td>52%</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2012</td>
      <td>7-May</td>
      <td>8-Nov</td>
      <td>20-Apr</td>
      <td>8-Nov</td>
      <td>No closure</td>
      <td>No closure</td>
      <td>43%</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2011 *</td>
      <td>18-Jun</td>
      <td>17-Jan</td>
      <td>27-May</td>
      <td>19-Nov</td>
      <td>15-Apr</td>
      <td>No closure</td>
      <td>178%</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2010</td>
      <td>5-Jun</td>
      <td>19-Nov</td>
      <td>29-May</td>
      <td>7-Nov</td>
      <td>21-May</td>
      <td>20-Nov</td>
      <td>107%</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2009</td>
      <td>19-May</td>
      <td>12-Nov</td>
      <td>5-May</td>
      <td>12-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>92%</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2008</td>
      <td>21-May</td>
      <td>30-Oct</td>
      <td>2-May</td>
      <td>12-Dec</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>99%</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2007</td>
      <td>11-May</td>
      <td>6-Dec</td>
      <td>4-May</td>
      <td>6-Dec</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>46%</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2006</td>
      <td>17-Jun</td>
      <td>27-Nov</td>
      <td>25-May</td>
      <td>27-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>129%</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2005</td>
      <td>24-Jun</td>
      <td>25-Nov</td>
      <td>25-May</td>
      <td>?</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>163%</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2004</td>
      <td>14-May</td>
      <td>17-Oct</td>
      <td>14-May</td>
      <td>?</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>83%</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2003</td>
      <td>31-May</td>
      <td>31-Oct</td>
      <td>31-May</td>
      <td>31-Oct</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>65%</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2002</td>
      <td>22-May</td>
      <td>5-Nov</td>
      <td>17-May</td>
      <td>5-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>95%</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2001</td>
      <td>12-May</td>
      <td>11-Nov</td>
      <td>15-May</td>
      <td>?</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>67%</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2000</td>
      <td>18-May</td>
      <td>9-Nov</td>
      <td>15-May</td>
      <td>9-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>97%</td>
    </tr>
    <tr>
      <th>21</th>
      <td>1999 *</td>
      <td>28-May</td>
      <td>23-Nov</td>
      <td>28-May</td>
      <td>23-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>110%</td>
    </tr>
    <tr>
      <th>22</th>
      <td>1998</td>
      <td>1-Jul</td>
      <td>12-Nov</td>
      <td>1-Jul</td>
      <td>6-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>156%</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1997</td>
      <td>13-Jun</td>
      <td>12-Nov</td>
      <td>22-May</td>
      <td>12-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>105%</td>
    </tr>
    <tr>
      <th>24</th>
      <td>1996</td>
      <td>31-May</td>
      <td>5-Nov</td>
      <td>24-May</td>
      <td>5-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>111%</td>
    </tr>
    <tr>
      <th>25</th>
      <td>1995</td>
      <td>30-Jun</td>
      <td>11-Dec</td>
      <td>1-Jul</td>
      <td>11-Dec</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>178%</td>
    </tr>
    <tr>
      <th>26</th>
      <td>1994</td>
      <td>25-May</td>
      <td>10-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>51%</td>
    </tr>
    <tr>
      <th>27</th>
      <td>1993</td>
      <td>3-Jun</td>
      <td>24-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>159%</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1992</td>
      <td>15-May</td>
      <td>10-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>58%</td>
    </tr>
    <tr>
      <th>29</th>
      <td>1991</td>
      <td>26-May</td>
      <td>14-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>79%</td>
    </tr>
    <tr>
      <th>30</th>
      <td>1990</td>
      <td>17-May</td>
      <td>19-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45%</td>
    </tr>
    <tr>
      <th>31</th>
      <td>1989</td>
      <td>12-May</td>
      <td>24-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>83%</td>
    </tr>
    <tr>
      <th>32</th>
      <td>1988</td>
      <td>29-Apr</td>
      <td>14-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>31%</td>
    </tr>
    <tr>
      <th>33</th>
      <td>1987</td>
      <td>2-May</td>
      <td>13-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>51%</td>
    </tr>
    <tr>
      <th>34</th>
      <td>1986</td>
      <td>24-May</td>
      <td>29-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>137%</td>
    </tr>
    <tr>
      <th>35</th>
      <td>1985</td>
      <td>8-May</td>
      <td>12-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>97%</td>
    </tr>
    <tr>
      <th>36</th>
      <td>1984</td>
      <td>19-May</td>
      <td>8-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>85%</td>
    </tr>
    <tr>
      <th>37</th>
      <td>1983</td>
      <td>29-Jun</td>
      <td>11-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>224%</td>
    </tr>
    <tr>
      <th>38</th>
      <td>1982</td>
      <td>28-May</td>
      <td>15-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>131%</td>
    </tr>
    <tr>
      <th>39</th>
      <td>1981</td>
      <td>15-May</td>
      <td>12-Nov</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>77%</td>
    </tr>
    <tr>
      <th>40</th>
      <td>1980</td>
      <td>6-Jun</td>
      <td>2-Dec</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>144%</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Average\n('96-'15)</td>
      <td>26-May</td>
      <td>14-Nov</td>
      <td>14-May</td>
      <td>15-Nov</td>
      <td>--</td>
      <td>--</td>
      <td>92%</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Median\n('96-'15)</td>
      <td>21-May</td>
      <td>12-Nov</td>
      <td>16-May</td>
      <td>10-Nov</td>
      <td>--</td>
      <td>--</td>
      <td>96%</td>
    </tr>
  </tbody>
</table>
</div>



The only columns needed for analysis are "Year" and "Tioga Opened," and the other columns can be dropped.

Using April 1st as a reference date, I created the function formatDates() to calculate the number of days since April 1st that Tioga Pass opened for each year, appending to the new column "Days Since Apr 1."


```python
import datetime

df = df.drop([41, 42])
df = df.drop(columns=['Tioga Closed', 'Glacier Pt Opened', 'Glacier Pt Closed', 'Mariposa Grove Opened', 'Mariposa Grove Closed', 'Snowpack as of Apr 1'])
df['Days Since Apr 1'] = 0

def formatDates(row):
    snowpack_day = datetime.datetime.strptime('1900-04-01 00:00:00', '%Y-%m-%d %H:%M:%S')
    tioga_open = datetime.datetime.strptime(row, '%d-%b')
    days_since = tioga_open - snowpack_day
    return days_since.days

for i in range(len(df)):
    df.iloc[i, 2] = formatDates(df.iloc[i, 1])

df
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
      <th>Year</th>
      <th>Tioga Opened</th>
      <th>Days Since Apr 1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020 *</td>
      <td>15-Jun</td>
      <td>75</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2019 *</td>
      <td>1-Jul</td>
      <td>91</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018 *</td>
      <td>21-May</td>
      <td>50</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017 *</td>
      <td>29-Jun</td>
      <td>89</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016 *</td>
      <td>18-May</td>
      <td>47</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015 *</td>
      <td>4-May</td>
      <td>33</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2014 *</td>
      <td>2-May</td>
      <td>31</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2013</td>
      <td>11-May</td>
      <td>40</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2012</td>
      <td>7-May</td>
      <td>36</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2011 *</td>
      <td>18-Jun</td>
      <td>78</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2010</td>
      <td>5-Jun</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2009</td>
      <td>19-May</td>
      <td>48</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2008</td>
      <td>21-May</td>
      <td>50</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2007</td>
      <td>11-May</td>
      <td>40</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2006</td>
      <td>17-Jun</td>
      <td>77</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2005</td>
      <td>24-Jun</td>
      <td>84</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2004</td>
      <td>14-May</td>
      <td>43</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2003</td>
      <td>31-May</td>
      <td>60</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2002</td>
      <td>22-May</td>
      <td>51</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2001</td>
      <td>12-May</td>
      <td>41</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2000</td>
      <td>18-May</td>
      <td>47</td>
    </tr>
    <tr>
      <th>21</th>
      <td>1999 *</td>
      <td>28-May</td>
      <td>57</td>
    </tr>
    <tr>
      <th>22</th>
      <td>1998</td>
      <td>1-Jul</td>
      <td>91</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1997</td>
      <td>13-Jun</td>
      <td>73</td>
    </tr>
    <tr>
      <th>24</th>
      <td>1996</td>
      <td>31-May</td>
      <td>60</td>
    </tr>
    <tr>
      <th>25</th>
      <td>1995</td>
      <td>30-Jun</td>
      <td>90</td>
    </tr>
    <tr>
      <th>26</th>
      <td>1994</td>
      <td>25-May</td>
      <td>54</td>
    </tr>
    <tr>
      <th>27</th>
      <td>1993</td>
      <td>3-Jun</td>
      <td>63</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1992</td>
      <td>15-May</td>
      <td>44</td>
    </tr>
    <tr>
      <th>29</th>
      <td>1991</td>
      <td>26-May</td>
      <td>55</td>
    </tr>
    <tr>
      <th>30</th>
      <td>1990</td>
      <td>17-May</td>
      <td>46</td>
    </tr>
    <tr>
      <th>31</th>
      <td>1989</td>
      <td>12-May</td>
      <td>41</td>
    </tr>
    <tr>
      <th>32</th>
      <td>1988</td>
      <td>29-Apr</td>
      <td>28</td>
    </tr>
    <tr>
      <th>33</th>
      <td>1987</td>
      <td>2-May</td>
      <td>31</td>
    </tr>
    <tr>
      <th>34</th>
      <td>1986</td>
      <td>24-May</td>
      <td>53</td>
    </tr>
    <tr>
      <th>35</th>
      <td>1985</td>
      <td>8-May</td>
      <td>37</td>
    </tr>
    <tr>
      <th>36</th>
      <td>1984</td>
      <td>19-May</td>
      <td>48</td>
    </tr>
    <tr>
      <th>37</th>
      <td>1983</td>
      <td>29-Jun</td>
      <td>89</td>
    </tr>
    <tr>
      <th>38</th>
      <td>1982</td>
      <td>28-May</td>
      <td>57</td>
    </tr>
    <tr>
      <th>39</th>
      <td>1981</td>
      <td>15-May</td>
      <td>44</td>
    </tr>
    <tr>
      <th>40</th>
      <td>1980</td>
      <td>6-Jun</td>
      <td>66</td>
    </tr>
  </tbody>
</table>
</div>



The snow depth data dates back to 2005, so the Tioga Pass opening dates can be reduced to 2005-2020.


```python
# Drops the years before 2005, and reverses the dataframe so data is sorted from old --> new.
df = df[0:16]
df = df[::-1].reset_index(drop=True)
df
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
      <th>Year</th>
      <th>Tioga Opened</th>
      <th>Days Since Apr 1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2005</td>
      <td>24-Jun</td>
      <td>84</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2006</td>
      <td>17-Jun</td>
      <td>77</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2007</td>
      <td>11-May</td>
      <td>40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2008</td>
      <td>21-May</td>
      <td>50</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2009</td>
      <td>19-May</td>
      <td>48</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2010</td>
      <td>5-Jun</td>
      <td>65</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2011 *</td>
      <td>18-Jun</td>
      <td>78</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2012</td>
      <td>7-May</td>
      <td>36</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2013</td>
      <td>11-May</td>
      <td>40</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2014 *</td>
      <td>2-May</td>
      <td>31</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2015 *</td>
      <td>4-May</td>
      <td>33</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2016 *</td>
      <td>18-May</td>
      <td>47</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2017 *</td>
      <td>29-Jun</td>
      <td>89</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2018 *</td>
      <td>21-May</td>
      <td>50</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2019 *</td>
      <td>1-Jul</td>
      <td>91</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2020 *</td>
      <td>15-Jun</td>
      <td>75</td>
    </tr>
  </tbody>
</table>
</div>



Next, let's import the snow depth data from the [California Data Exchange Center](http://cdec4gov.water.ca.gov/dynamicapp/selectQuery). The station of interest is in Tuolumne Meadows (TUM).


```python
import pandas as pd
df_TUM = pd.read_excel('.../TUM_18.xlsx')
df_TUM
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
      <th>STATION_ID</th>
      <th>DURATION</th>
      <th>SENSOR_NUMBER</th>
      <th>SENS_TYPE</th>
      <th>DATE TIME</th>
      <th>OBS DATE</th>
      <th>VALUE</th>
      <th>DATA_FLAG</th>
      <th>UNITS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>TUM</td>
      <td>D</td>
      <td>18</td>
      <td>SNOW DP</td>
      <td>NaN</td>
      <td>20041001.0</td>
      <td>2.0</td>
      <td></td>
      <td>INCHES</td>
    </tr>
    <tr>
      <th>1</th>
      <td>TUM</td>
      <td>D</td>
      <td>18</td>
      <td>SNOW DP</td>
      <td>NaN</td>
      <td>20041002.0</td>
      <td>0.0</td>
      <td></td>
      <td>INCHES</td>
    </tr>
    <tr>
      <th>2</th>
      <td>TUM</td>
      <td>D</td>
      <td>18</td>
      <td>SNOW DP</td>
      <td>NaN</td>
      <td>20041003.0</td>
      <td>-0.0</td>
      <td></td>
      <td>INCHES</td>
    </tr>
    <tr>
      <th>3</th>
      <td>TUM</td>
      <td>D</td>
      <td>18</td>
      <td>SNOW DP</td>
      <td>NaN</td>
      <td>20041004.0</td>
      <td>0.0</td>
      <td></td>
      <td>INCHES</td>
    </tr>
    <tr>
      <th>4</th>
      <td>TUM</td>
      <td>D</td>
      <td>18</td>
      <td>SNOW DP</td>
      <td>NaN</td>
      <td>20041005.0</td>
      <td>1.0</td>
      <td></td>
      <td>INCHES</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>6004</th>
      <td>TUM</td>
      <td>D</td>
      <td>18</td>
      <td>SNOW DP</td>
      <td>NaN</td>
      <td>20210310.0</td>
      <td>38.0</td>
      <td></td>
      <td>INCHES</td>
    </tr>
    <tr>
      <th>6005</th>
      <td>TUM</td>
      <td>D</td>
      <td>18</td>
      <td>SNOW DP</td>
      <td>NaN</td>
      <td>20210311.0</td>
      <td>118.0</td>
      <td></td>
      <td>INCHES</td>
    </tr>
    <tr>
      <th>6006</th>
      <td>TUM</td>
      <td>D</td>
      <td>18</td>
      <td>SNOW DP</td>
      <td>NaN</td>
      <td>20210312.0</td>
      <td>118.0</td>
      <td></td>
      <td>INCHES</td>
    </tr>
    <tr>
      <th>6007</th>
      <td>TUM</td>
      <td>D</td>
      <td>18</td>
      <td>SNOW DP</td>
      <td>NaN</td>
      <td>20210313.0</td>
      <td>42.0</td>
      <td></td>
      <td>INCHES</td>
    </tr>
    <tr>
      <th>6008</th>
      <td>TUM</td>
      <td>D</td>
      <td>18</td>
      <td>SNOW DP</td>
      <td>NaN</td>
      <td>20210314.0</td>
      <td>NaN</td>
      <td></td>
      <td>INCHES</td>
    </tr>
  </tbody>
</table>
<p>6009 rows × 9 columns</p>
</div>



The only columns needed for analysis are "OBS DATE" and "VALUE." "DATE TIME" can also be kept, since we'll need to convert the OBS DATE into a datetime object.

Other columns can be dropped, and any rows with missing snow data can also be dropped.


```python
# Drops the columns that are no longer needed.
# Drops rows with NaN values in the VALUE or OBS DATE columns
df_TUM = df_TUM.drop(columns=['STATION_ID', 'DURATION', 'SENSOR_NUMBER', 'SENS_TYPE', 'DATA_FLAG', 'UNITS'])
df_TUM = df_TUM.dropna(subset=['VALUE']).reset_index(drop=True)
df_TUM = df_TUM.dropna(subset=['OBS DATE']).reset_index(drop=True)
df_TUM
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
      <th>DATE TIME</th>
      <th>OBS DATE</th>
      <th>VALUE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>20041001.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>20041002.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>20041003.0</td>
      <td>-0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>20041004.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>20041005.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>5432</th>
      <td>NaN</td>
      <td>20210309.0</td>
      <td>36.0</td>
    </tr>
    <tr>
      <th>5433</th>
      <td>NaN</td>
      <td>20210310.0</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>5434</th>
      <td>NaN</td>
      <td>20210311.0</td>
      <td>118.0</td>
    </tr>
    <tr>
      <th>5435</th>
      <td>NaN</td>
      <td>20210312.0</td>
      <td>118.0</td>
    </tr>
    <tr>
      <th>5436</th>
      <td>NaN</td>
      <td>20210313.0</td>
      <td>42.0</td>
    </tr>
  </tbody>
</table>
<p>5437 rows × 3 columns</p>
</div>




```python
# Convert the OBS DATE column to string format
df_TUM['OBS DATE'] = df_TUM['OBS DATE'].astype(int)
df_TUM['OBS DATE'] = df_TUM['OBS DATE'].astype(str)

# Adds on the DATE TIME column by converting the string form of OBS DATE to pandas TimeStamp object
df_TUM['DATE TIME'] = pd.to_datetime(df_TUM['OBS DATE'], format='%Y%m%d')
df_TUM
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
      <th>DATE TIME</th>
      <th>OBS DATE</th>
      <th>VALUE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2004-10-01</td>
      <td>20041001</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2004-10-02</td>
      <td>20041002</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2004-10-03</td>
      <td>20041003</td>
      <td>-0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2004-10-04</td>
      <td>20041004</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2004-10-05</td>
      <td>20041005</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>5432</th>
      <td>2021-03-09</td>
      <td>20210309</td>
      <td>36.0</td>
    </tr>
    <tr>
      <th>5433</th>
      <td>2021-03-10</td>
      <td>20210310</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>5434</th>
      <td>2021-03-11</td>
      <td>20210311</td>
      <td>118.0</td>
    </tr>
    <tr>
      <th>5435</th>
      <td>2021-03-12</td>
      <td>20210312</td>
      <td>118.0</td>
    </tr>
    <tr>
      <th>5436</th>
      <td>2021-03-13</td>
      <td>20210313</td>
      <td>42.0</td>
    </tr>
  </tbody>
</table>
<p>5437 rows × 3 columns</p>
</div>



With the daily snow depth data from 2004-2020, let's average the snow depth data for each month.


```python
# Groupby the month and year
TUM_avg = df_TUM.groupby([(df_TUM['DATE TIME'].dt.year),(df_TUM['DATE TIME'].dt.month)]).mean()
TUM_avg
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
      <th></th>
      <th>VALUE</th>
    </tr>
    <tr>
      <th>DATE TIME</th>
      <th>DATE TIME</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">2004</th>
      <th>10</th>
      <td>9.833333</td>
    </tr>
    <tr>
      <th>11</th>
      <td>22.166667</td>
    </tr>
    <tr>
      <th>12</th>
      <td>35.258065</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">2005</th>
      <th>1</th>
      <td>78.064516</td>
    </tr>
    <tr>
      <th>2</th>
      <td>78.250000</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">2020</th>
      <th>11</th>
      <td>15.033333</td>
    </tr>
    <tr>
      <th>12</th>
      <td>24.258065</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">2021</th>
      <th>1</th>
      <td>33.838710</td>
    </tr>
    <tr>
      <th>2</th>
      <td>50.642857</td>
    </tr>
    <tr>
      <th>3</th>
      <td>50.538462</td>
    </tr>
  </tbody>
</table>
<p>196 rows × 1 columns</p>
</div>



Once the snow depth data has been averaged, let's group the data by month. For example, the TUM_1 dataframe will include the average snow depth for each January from 2005-2020.


```python
# Set the name of the multiindex
TUM_avg.index.names = ['Year', 'Month']

# Select January subset from the multiindex dataframe
TUM_1 = TUM_avg[TUM_avg.index.get_level_values('Month') == 1]
TUM_1
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
      <th></th>
      <th>VALUE</th>
    </tr>
    <tr>
      <th>Year</th>
      <th>Month</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2005</th>
      <th>1</th>
      <td>78.064516</td>
    </tr>
    <tr>
      <th>2006</th>
      <th>1</th>
      <td>70.058824</td>
    </tr>
    <tr>
      <th>2007</th>
      <th>1</th>
      <td>20.483871</td>
    </tr>
    <tr>
      <th>2008</th>
      <th>1</th>
      <td>54.870968</td>
    </tr>
    <tr>
      <th>2009</th>
      <th>1</th>
      <td>27.774194</td>
    </tr>
    <tr>
      <th>2010</th>
      <th>1</th>
      <td>44.800000</td>
    </tr>
    <tr>
      <th>2011</th>
      <th>1</th>
      <td>66.428571</td>
    </tr>
    <tr>
      <th>2012</th>
      <th>1</th>
      <td>8.178571</td>
    </tr>
    <tr>
      <th>2013</th>
      <th>1</th>
      <td>54.407407</td>
    </tr>
    <tr>
      <th>2014</th>
      <th>1</th>
      <td>4.933333</td>
    </tr>
    <tr>
      <th>2015</th>
      <th>1</th>
      <td>8.866667</td>
    </tr>
    <tr>
      <th>2016</th>
      <th>1</th>
      <td>51.137931</td>
    </tr>
    <tr>
      <th>2017</th>
      <th>1</th>
      <td>73.782609</td>
    </tr>
    <tr>
      <th>2018</th>
      <th>1</th>
      <td>24.483871</td>
    </tr>
    <tr>
      <th>2019</th>
      <th>1</th>
      <td>49.580645</td>
    </tr>
    <tr>
      <th>2020</th>
      <th>1</th>
      <td>29.129032</td>
    </tr>
    <tr>
      <th>2021</th>
      <th>1</th>
      <td>33.838710</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Repeat for all 12 months
TUM_2 = TUM_avg[TUM_avg.index.get_level_values('Month') == 2]
TUM_3 = TUM_avg[TUM_avg.index.get_level_values('Month') == 3]
TUM_4 = TUM_avg[TUM_avg.index.get_level_values('Month') == 4]
TUM_5 = TUM_avg[TUM_avg.index.get_level_values('Month') == 5]
TUM_6 = TUM_avg[TUM_avg.index.get_level_values('Month') == 6]
TUM_7 = TUM_avg[TUM_avg.index.get_level_values('Month') == 7]
TUM_11 = TUM_avg[TUM_avg.index.get_level_values('Month') == 11]
TUM_12 = TUM_avg[TUM_avg.index.get_level_values('Month') == 12]
```

Given that the snow depth data has been averaged for each of the 12 months spanning 2005-2020, we can create a subset of the TUM_3 dataframe that excludes 2021 data.


```python
TUM_3_Historical = TUM_3[TUM_3.index.get_level_values('Year') != 2021]
TUM_3_Historical
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
      <th></th>
      <th>VALUE</th>
    </tr>
    <tr>
      <th>Year</th>
      <th>Month</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2005</th>
      <th>3</th>
      <td>81.548387</td>
    </tr>
    <tr>
      <th>2006</th>
      <th>3</th>
      <td>89.200000</td>
    </tr>
    <tr>
      <th>2007</th>
      <th>3</th>
      <td>31.225806</td>
    </tr>
    <tr>
      <th>2008</th>
      <th>3</th>
      <td>55.645161</td>
    </tr>
    <tr>
      <th>2009</th>
      <th>3</th>
      <td>58.387097</td>
    </tr>
    <tr>
      <th>2010</th>
      <th>3</th>
      <td>66.548387</td>
    </tr>
    <tr>
      <th>2011</th>
      <th>3</th>
      <td>83.333333</td>
    </tr>
    <tr>
      <th>2012</th>
      <th>3</th>
      <td>20.793103</td>
    </tr>
    <tr>
      <th>2013</th>
      <th>3</th>
      <td>37.000000</td>
    </tr>
    <tr>
      <th>2014</th>
      <th>3</th>
      <td>19.724138</td>
    </tr>
    <tr>
      <th>2015</th>
      <th>3</th>
      <td>1.064516</td>
    </tr>
    <tr>
      <th>2016</th>
      <th>3</th>
      <td>44.566667</td>
    </tr>
    <tr>
      <th>2017</th>
      <th>3</th>
      <td>97.516129</td>
    </tr>
    <tr>
      <th>2018</th>
      <th>3</th>
      <td>50.709677</td>
    </tr>
    <tr>
      <th>2019</th>
      <th>3</th>
      <td>93.870968</td>
    </tr>
    <tr>
      <th>2020</th>
      <th>3</th>
      <td>34.709677</td>
    </tr>
  </tbody>
</table>
</div>



# Plotting the Data

Now that the data has been processed, it's time to plot the data and build the model. A simple linear regression between Days Since April 1st and Snow Depth in March can be performed.


```python
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression

x = TUM_3_Historical['VALUE'].values.reshape(-1, 1)
y = df['Days Since Apr 1'].values.reshape(-1, 1)

linear_regressor = LinearRegression()  # Create object for the class
linear_regressor.fit(x, y)  # Perform linear regression
y_pred = linear_regressor.predict(x)  # Make predictions

plt.plot(x, y_pred, color='red')
plt.scatter(x, y)
plt.show()
```


    
![Tioga Pass LSR Model](/assets/images/tioga_pass_lsr_model.png)
    



```python
from scipy.stats import linregress
slope, intercept, r_value, p_value, std_err = linregress(x.flatten().tolist(), y.flatten().tolist())
results = linregress(x.flatten().tolist(), y.flatten().tolist())
print(results)
print('R-squared:', r_value**2)
```

    LinregressResult(slope=0.6338435941606729, intercept=24.074433161488514, rvalue=0.8816178208666444, pvalue=6.354407547787794e-06, stderr=0.09068732698031783, intercept_stderr=5.541187818860552)
    R-squared: 0.7772499820696507


The scatterplot shows a moderately strong, positive, linear association between Days Since April 1st and Snow Depth in March, with one potential outlier. 77.7% of the variability in Days Since April 1st is accounted by the LSR model on Snow Depth in March.

With the LRS model, we can approximate the number of Days Since April 1st that Tioga Pass will open this year based on the Snow Depth data for March 2021.


```python
current_snow_depth = TUM_3['VALUE'].iloc[-1]
print(current_snow_depth, 'inches')

predicted_days = slope*current_snow_depth + intercept
print(np.round(predicted_days), 'days since April 1')
```

    50.53846153846154 inches
    56.0 days since April 1



```python
raw_date = datetime.date(2021, 4, 1) + datetime.timedelta(np.round(predicted_days))
print(raw_date)
```

    2021-05-27


Historically, NPS has always opened Tioga Pass on a Monday. As such, May 27 needs to be rounded to the following Monday.


```python
import datetime
def nextMonday(date):
    monday = 0
    days_ahead = monday - date.weekday() + 7
    return date + datetime.timedelta(days_ahead)

predicted_date = nextMonday(raw_date)
print(predicted_date)
```

    2021-05-31

# Conclusion

Based on the snow depth data up to March 13, 2021, my prediction for this year's Tioga Pass Opening Date is May 31, 2021.