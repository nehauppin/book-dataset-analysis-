## Book Dataset Analysis 
Neha Uppin

### Outline

### Importing 


```python
import pandas as pd 
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline 
```


```python
df = pd.read_csv('Amazon-books.csv')

df.head()
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
      <th>Title</th>
      <th>Rank</th>
      <th>Reviews</th>
      <th>Review Count</th>
      <th>Price</th>
      <th>Genre</th>
      <th>Manufacturer</th>
      <th>Brand</th>
      <th>Author</th>
      <th>Number of Pages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fourth Wing (The Empyrean, 1)</td>
      <td>1</td>
      <td>4.8</td>
      <td>135916</td>
      <td>18.69</td>
      <td>Fantasy</td>
      <td>Entangled: Red Tower Books</td>
      <td>Macmillan</td>
      <td>Rebecca Yarros</td>
      <td>528.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Atomic Habits: An Easy &amp; Proven Way to Build G...</td>
      <td>2</td>
      <td>4.8</td>
      <td>120356</td>
      <td>12.50</td>
      <td>Personal Transformation</td>
      <td>Avery</td>
      <td>Avery</td>
      <td>James Clear</td>
      <td>320.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Iron Flame (The Empyrean, 2)</td>
      <td>3</td>
      <td>4.7</td>
      <td>79851</td>
      <td>14.78</td>
      <td>Epic</td>
      <td>Entangled: Red Tower Books</td>
      <td>Kiligry</td>
      <td>Rebecca Yarros</td>
      <td>640.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Dinner Tonight: 100 Simple, Healthy Recipes fo...</td>
      <td>4</td>
      <td>4.1</td>
      <td>6</td>
      <td>26.00</td>
      <td>Natural Foods</td>
      <td>William Morrow Cookbooks</td>
      <td>NaN</td>
      <td>Alex Snodgrass</td>
      <td>256.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Oath and Honor: A Memoir and a Warning</td>
      <td>5</td>
      <td>4.8</td>
      <td>3536</td>
      <td>21.49</td>
      <td>Political</td>
      <td>Little, Brown and Company</td>
      <td>NaN</td>
      <td>Liz Cheney</td>
      <td>384.0</td>
    </tr>
  </tbody>
</table>
</div>



### Profiling

#### Data Structure Overview
This dataset has 4846 rows and 10 columns, with a mix of numeric and categorical data types. All the columns seem to stored as an appropriate type, however, I would make the change to store 'Number of Pages' as an integer, because it is unlikely to have a fraction of a page in a book. 

Looking at numeric statistics, the book prices range dramatically from 0.15 to 199.9. The mean at 13.10 and the median is at 11.10. The higher mean could indicate that there are some high-value outliers pulling the average upwards. The number of book pages range from 1 to 5280. A book with 1 page seems highly unlikely, it would be interesting to see what these entries are. 

Looking at statistics for all columns, the most common genre being Fantasy, with 176 occurences. It also looks like some repeat titles, which could indicate different editions of the same book, the book being in different formats (hardcover vs. paperback), or even different books with the same title. 


```python
# overview of dataframe
display(df.info())

# numeric stats
display(df.describe().round(2))

# stats for all 
display(df.describe(include='all'))
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 4846 entries, 0 to 4845
    Data columns (total 10 columns):
     #   Column           Non-Null Count  Dtype  
    ---  ------           --------------  -----  
     0   Title            4846 non-null   object 
     1   Rank             4846 non-null   int64  
     2   Reviews          4846 non-null   float64
     3   Review Count     4846 non-null   int64  
     4   Price            4846 non-null   float64
     5   Genre            4846 non-null   object 
     6   Manufacturer     4846 non-null   object 
     7   Brand            3144 non-null   object 
     8   Author           4846 non-null   object 
     9   Number of Pages  4775 non-null   float64
    dtypes: float64(3), int64(2), object(5)
    memory usage: 378.7+ KB
    


    None



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
      <th>Rank</th>
      <th>Reviews</th>
      <th>Review Count</th>
      <th>Price</th>
      <th>Number of Pages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>4846.00</td>
      <td>4846.00</td>
      <td>4846.00</td>
      <td>4846.00</td>
      <td>4775.00</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>2533.39</td>
      <td>4.66</td>
      <td>12735.63</td>
      <td>13.10</td>
      <td>347.74</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1500.59</td>
      <td>0.23</td>
      <td>28780.36</td>
      <td>10.25</td>
      <td>415.87</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>0.15</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1242.75</td>
      <td>4.60</td>
      <td>943.50</td>
      <td>7.41</td>
      <td>128.00</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>2501.50</td>
      <td>4.70</td>
      <td>4010.00</td>
      <td>11.10</td>
      <td>272.00</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>3768.75</td>
      <td>4.80</td>
      <td>12033.00</td>
      <td>15.67</td>
      <td>408.00</td>
    </tr>
    <tr>
      <th>max</th>
      <td>15176.00</td>
      <td>5.00</td>
      <td>621499.00</td>
      <td>199.99</td>
      <td>5280.00</td>
    </tr>
  </tbody>
</table>
</div>



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
      <th>Title</th>
      <th>Rank</th>
      <th>Reviews</th>
      <th>Review Count</th>
      <th>Price</th>
      <th>Genre</th>
      <th>Manufacturer</th>
      <th>Brand</th>
      <th>Author</th>
      <th>Number of Pages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>4846</td>
      <td>4846.000000</td>
      <td>4846.000000</td>
      <td>4846.000000</td>
      <td>4846.000000</td>
      <td>4846</td>
      <td>4846</td>
      <td>3144</td>
      <td>4846</td>
      <td>4775.000000</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>4758</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>907</td>
      <td>972</td>
      <td>758</td>
      <td>2901</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>top</th>
      <td>Goodnight Moon</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Fantasy</td>
      <td>Independently published</td>
      <td>Scholastic</td>
      <td>Calendars Workman</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>176</td>
      <td>345</td>
      <td>98</td>
      <td>40</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>NaN</td>
      <td>2533.388774</td>
      <td>4.662299</td>
      <td>12735.633306</td>
      <td>13.098601</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>347.739686</td>
    </tr>
    <tr>
      <th>std</th>
      <td>NaN</td>
      <td>1500.594167</td>
      <td>0.225194</td>
      <td>28780.356812</td>
      <td>10.248512</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>415.874433</td>
    </tr>
    <tr>
      <th>min</th>
      <td>NaN</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.150000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>NaN</td>
      <td>1242.750000</td>
      <td>4.600000</td>
      <td>943.500000</td>
      <td>7.412500</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>128.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>NaN</td>
      <td>2501.500000</td>
      <td>4.700000</td>
      <td>4010.000000</td>
      <td>11.100000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>272.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>NaN</td>
      <td>3768.750000</td>
      <td>4.800000</td>
      <td>12033.000000</td>
      <td>15.667500</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>408.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>NaN</td>
      <td>15176.000000</td>
      <td>5.000000</td>
      <td>621499.000000</td>
      <td>199.990000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5280.000000</td>
    </tr>
  </tbody>
</table>
</div>


#### Data Quality Overview
Most of the data is complete, except for 'Brand', which has 1702 null values and 'Pages' which has 71 null values.

It looks like none of the columns have unique values, which makes sense for most columns such as price, genre, author and number of pages. As mentioned before, there are a few reason why titles are not unique. It is quite interesting why the ranks are not unique and it looks like there are 819 books that have duplicate ranks. Since it is unsure how often this data was collected (weekly, monthly), we only know that it covers the beginning to the end of 2023, so it could be because books held different ranks at different times of the year. 


```python
df['Rank'].value_counts()
df[df['Rank'] == 3396]
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
      <th>Title</th>
      <th>Rank</th>
      <th>Reviews</th>
      <th>Review Count</th>
      <th>Price</th>
      <th>Genre</th>
      <th>Manufacturer</th>
      <th>Brand</th>
      <th>Author</th>
      <th>Number of Pages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3268</th>
      <td>Everything Is F*cked</td>
      <td>3396</td>
      <td>4.6</td>
      <td>11941</td>
      <td>10.81</td>
      <td>Happiness</td>
      <td>Harper Paperbacks</td>
      <td>Harper Paperbacks</td>
      <td>Mark Manson</td>
      <td>288.0</td>
    </tr>
    <tr>
      <th>3269</th>
      <td>My First 100 Words - Mis Primeras 100 Palabras...</td>
      <td>3396</td>
      <td>4.8</td>
      <td>1549</td>
      <td>5.91</td>
      <td>Spanish</td>
      <td>Parragon Books</td>
      <td>Parragon Books</td>
      <td>Press Cottage</td>
      <td>32.0</td>
    </tr>
    <tr>
      <th>3270</th>
      <td>Animal Crossing: New Horizons 2024 Day-to-Day ...</td>
      <td>3396</td>
      <td>4.5</td>
      <td>23</td>
      <td>13.82</td>
      <td>Video Games</td>
      <td>Harry N Abrams Inc.</td>
      <td>NaN</td>
      <td>Nintendo Nintendo</td>
      <td>740.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# missing values per column
display(df.isnull().sum())

# distinct values per column
display(df.nunique())

# duplicate values per column 
print('Number of duplicates per column')
for col in df.columns:
    duplicates = df[col].duplicated().sum()
    print(f'{col}: {duplicates}')
```


    Title                 0
    Rank                  0
    Reviews               0
    Review Count          0
    Price                 0
    Genre                 0
    Manufacturer          0
    Brand              1702
    Author                0
    Number of Pages      71
    dtype: int64



    Title              4758
    Rank               4027
    Reviews              24
    Review Count       3764
    Price              1741
    Genre               907
    Manufacturer        972
    Brand               758
    Author             2901
    Number of Pages     630
    dtype: int64


    Number of duplicates per column
    Title: 88
    Rank: 819
    Reviews: 4822
    Review Count: 1082
    Price: 3105
    Genre: 3939
    Manufacturer: 3874
    Brand: 4087
    Author: 1945
    Number of Pages: 4215
    

### Data Cleaning
- Renamed the 'Reviews' column to 'Rating' for clarity
- Changed the data type to integer for 'Number of Pages' because pages are whole numbers and this seems more logical


```python
# rename 'Reviews' to 'Rating'
df.rename(columns = {'Reviews' : 'Rating'}, inplace=True)

# change 'Number of Pages' dtype to an integer
df['Number of Pages'] = df['Number of Pages'].astype('Int64')

df.head()
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
      <th>Title</th>
      <th>Rank</th>
      <th>Rating</th>
      <th>Review Count</th>
      <th>Price</th>
      <th>Genre</th>
      <th>Manufacturer</th>
      <th>Brand</th>
      <th>Author</th>
      <th>Number of Pages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fourth Wing (The Empyrean, 1)</td>
      <td>1</td>
      <td>4.8</td>
      <td>135916</td>
      <td>18.69</td>
      <td>Fantasy</td>
      <td>Entangled: Red Tower Books</td>
      <td>Macmillan</td>
      <td>Rebecca Yarros</td>
      <td>528</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Atomic Habits: An Easy &amp; Proven Way to Build G...</td>
      <td>2</td>
      <td>4.8</td>
      <td>120356</td>
      <td>12.50</td>
      <td>Personal Transformation</td>
      <td>Avery</td>
      <td>Avery</td>
      <td>James Clear</td>
      <td>320</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Iron Flame (The Empyrean, 2)</td>
      <td>3</td>
      <td>4.7</td>
      <td>79851</td>
      <td>14.78</td>
      <td>Epic</td>
      <td>Entangled: Red Tower Books</td>
      <td>Kiligry</td>
      <td>Rebecca Yarros</td>
      <td>640</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Dinner Tonight: 100 Simple, Healthy Recipes fo...</td>
      <td>4</td>
      <td>4.1</td>
      <td>6</td>
      <td>26.00</td>
      <td>Natural Foods</td>
      <td>William Morrow Cookbooks</td>
      <td>NaN</td>
      <td>Alex Snodgrass</td>
      <td>256</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Oath and Honor: A Memoir and a Warning</td>
      <td>5</td>
      <td>4.8</td>
      <td>3536</td>
      <td>21.49</td>
      <td>Political</td>
      <td>Little, Brown and Company</td>
      <td>NaN</td>
      <td>Liz Cheney</td>
      <td>384</td>
    </tr>
  </tbody>
</table>
</div>



### Topic Specific Analysis
The following cells contain data analysis for Price, Rating and Genre

#### Price Analysis

The price distribution is positively skewed, with a majority of books being within the \$5-15 range. 

There is a dramatic decline after the \$25-50 mark, which indicates that books price above \\$50 are rare. 

When we actually calculate the upper and lower bounds, it looks like the upper bound is $28.05, so anything outside this is considered an outlier. When we look at these books, there are 232 entries that are beyond this. Most of these books seem to specialty items or box sets, which makes sense why they would be more expensive. 


```python
# plot book price distribution
plt.hist(df['Price'], bins=50, color='thistle', edgecolor='black', linewidth=0.5)
plt.title('Book Price Distribution')
plt.xlabel('Price ($)')
plt.ylabel('Number of Books')
```




    Text(0, 0.5, 'Number of Books')




    
![png](output_15_1.png)
    



```python
# calculate outlier boundaries using IQR
Q1 = df['Price'].quantile(0.25)
Q3 = df['Price'].quantile(0.75)
IQR = Q3 - Q1
upper = Q3 + 1.5 * IQR
lower = Q1 - 1.5 * IQR

print(f'Upper Bound: ${upper}')
print(f'Lower Bound: ${lower.round(2)}')

# find and display books outside the upper bound
books_upper = df[df['Price'] > upper]
books_upper
```

    Upper Bound: $28.05
    Lower Bound: $-4.97
    




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
      <th>Title</th>
      <th>Rank</th>
      <th>Rating</th>
      <th>Review Count</th>
      <th>Price</th>
      <th>Genre</th>
      <th>Manufacturer</th>
      <th>Brand</th>
      <th>Author</th>
      <th>Number of Pages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>51</th>
      <td>My Name Is Barbra</td>
      <td>53</td>
      <td>4.6</td>
      <td>2092</td>
      <td>30.56</td>
      <td>Movie Directors</td>
      <td>Viking</td>
      <td>NaN</td>
      <td>Barbra Streisand</td>
      <td>992</td>
    </tr>
    <tr>
      <th>52</th>
      <td>Harry Potter Paperback Box Set (Books 1-7)</td>
      <td>55</td>
      <td>4.9</td>
      <td>103150</td>
      <td>29.45</td>
      <td>School</td>
      <td>Scholastic Inc.</td>
      <td>Arthur A. Levine Books</td>
      <td>Rowling J</td>
      <td>&lt;NA&gt;</td>
    </tr>
    <tr>
      <th>53</th>
      <td>Hunger Games 4-Book Paperback Box Set (the Hun...</td>
      <td>56</td>
      <td>4.9</td>
      <td>3758</td>
      <td>37.18</td>
      <td>Difficult Discussions</td>
      <td>Scholastic Inc.</td>
      <td>NaN</td>
      <td>Suzanne Collins</td>
      <td>2720</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Berserk Deluxe Volume 1</td>
      <td>102</td>
      <td>4.9</td>
      <td>15172</td>
      <td>28.49</td>
      <td>Fantasy</td>
      <td>Dark Horse Manga</td>
      <td>Dark Horse Manga</td>
      <td>Jason DeAngelis</td>
      <td>696</td>
    </tr>
    <tr>
      <th>151</th>
      <td>The Lost Book of Herbal Remedies</td>
      <td>155</td>
      <td>4.7</td>
      <td>17266</td>
      <td>42.00</td>
      <td>Self-Help</td>
      <td>Global Brother</td>
      <td>Claude Davis</td>
      <td>Davis Claude</td>
      <td>304</td>
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
      <td>...</td>
    </tr>
    <tr>
      <th>4777</th>
      <td>The Twilight Saga Complete Collection</td>
      <td>5332</td>
      <td>4.7</td>
      <td>7188</td>
      <td>73.66</td>
      <td>Children's Books</td>
      <td>Little, Brown Books for Young Readers</td>
      <td>NaN</td>
      <td>Stephenie Meyer</td>
      <td>3520</td>
    </tr>
    <tr>
      <th>4796</th>
      <td>Japan: The Cookbook</td>
      <td>5443</td>
      <td>4.8</td>
      <td>1327</td>
      <td>35.99</td>
      <td>Japanese</td>
      <td>Phaidon Press</td>
      <td>Phaidon Press</td>
      <td>Hachisu Nancy</td>
      <td>464</td>
    </tr>
    <tr>
      <th>4799</th>
      <td>The Inheritance Games Collection</td>
      <td>5469</td>
      <td>4.8</td>
      <td>512</td>
      <td>32.53</td>
      <td>Children's Books</td>
      <td>Little, Brown Books for Young Readers</td>
      <td>NaN</td>
      <td>Jennifer Lynn Barnes</td>
      <td>1152</td>
    </tr>
    <tr>
      <th>4814</th>
      <td>Divergent Series Box Set (Books 1-4)</td>
      <td>5559</td>
      <td>4.8</td>
      <td>1666</td>
      <td>33.13</td>
      <td>Coming of Age</td>
      <td>Harper Collins Children’s Books</td>
      <td>HarperCollins Children</td>
      <td>Veronica Roth</td>
      <td>1616</td>
    </tr>
    <tr>
      <th>4822</th>
      <td>Basic Economics</td>
      <td>5608</td>
      <td>4.9</td>
      <td>4461</td>
      <td>28.49</td>
      <td>Economic Conditions</td>
      <td>Basic Books</td>
      <td>Basic Books</td>
      <td>Thomas Sowell</td>
      <td>704</td>
    </tr>
  </tbody>
</table>
<p>232 rows × 10 columns</p>
</div>



### Rating Analysis

Looking at just the top 10 highest rated books, all of them have a 5.0 rating. This doesn't necessarily mean they are the most popular because it also depends on the number of reviews the book has.

Instead, the top 25% most reviewed books were looked at. In this case, it was any books that had 12,033 or more reviews. By sorting the book titles that were within this threshold, we can look books with high ratings and a higher count of reviews. It eliminates the issue where a book with 5.0 stars from 1 review appears.


```python
# top 10 highest rated books
top_rated = df.nlargest(10, 'Rating')
top_rated
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
      <th>Title</th>
      <th>Rank</th>
      <th>Rating</th>
      <th>Review Count</th>
      <th>Price</th>
      <th>Genre</th>
      <th>Manufacturer</th>
      <th>Brand</th>
      <th>Author</th>
      <th>Number of Pages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>8</th>
      <td>Winter Turning: A Graphic Novel (Wings of Fire...</td>
      <td>9</td>
      <td>5.0</td>
      <td>1</td>
      <td>10.39</td>
      <td>Animals</td>
      <td>Graphix</td>
      <td>NaN</td>
      <td>Tui T. Sutherland</td>
      <td>224</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Ruthless Vows (Letters of Enchantment, 2)</td>
      <td>10</td>
      <td>5.0</td>
      <td>1</td>
      <td>14.98</td>
      <td>Romance</td>
      <td>Wednesday Books</td>
      <td>NaN</td>
      <td>Rebecca Ross</td>
      <td>432</td>
    </tr>
    <tr>
      <th>270</th>
      <td>Claudia and the Bad Joke: A Graphic Novel (The...</td>
      <td>280</td>
      <td>5.0</td>
      <td>1</td>
      <td>10.38</td>
      <td>Babysitting</td>
      <td>Graphix</td>
      <td>NaN</td>
      <td>Ann M. Martin</td>
      <td>192</td>
    </tr>
    <tr>
      <th>395</th>
      <td>Bob's Burgers 2024 Wall Calendar</td>
      <td>411</td>
      <td>5.0</td>
      <td>62</td>
      <td>12.79</td>
      <td>Performing Arts</td>
      <td>Rizzoli Universe</td>
      <td>Universe Publishing</td>
      <td>Inc. Twentieth</td>
      <td>24</td>
    </tr>
    <tr>
      <th>484</th>
      <td>More! More! More!</td>
      <td>500</td>
      <td>5.0</td>
      <td>333</td>
      <td>14.99</td>
      <td>Family Life</td>
      <td>Trufflery</td>
      <td>NaN</td>
      <td>Barbara Rieco</td>
      <td>38</td>
    </tr>
    <tr>
      <th>644</th>
      <td>Berserk Deluxe Volume 5</td>
      <td>668</td>
      <td>5.0</td>
      <td>5866</td>
      <td>29.53</td>
      <td>Fantasy</td>
      <td>Dark Horse Manga</td>
      <td>Dark Horse Manga</td>
      <td>Kentaro Miura</td>
      <td>720</td>
    </tr>
    <tr>
      <th>651</th>
      <td>Journey of Us: 101 Challenges for Couples</td>
      <td>674</td>
      <td>5.0</td>
      <td>1</td>
      <td>14.99</td>
      <td>Dating</td>
      <td>Independently published</td>
      <td>NaN</td>
      <td>Amour Editions</td>
      <td>205</td>
    </tr>
    <tr>
      <th>886</th>
      <td>Berserk Deluxe Volume 4</td>
      <td>912</td>
      <td>5.0</td>
      <td>6124</td>
      <td>33.73</td>
      <td>Fantasy</td>
      <td>Dark Horse Manga</td>
      <td>Dark Horse Manga</td>
      <td>Kentaro Miura</td>
      <td>704</td>
    </tr>
    <tr>
      <th>1204</th>
      <td>Berserk Deluxe Edition 7</td>
      <td>1233</td>
      <td>5.0</td>
      <td>3937</td>
      <td>31.49</td>
      <td>Fantasy</td>
      <td>Dark Horse Manga</td>
      <td>Dark Horse Manga</td>
      <td>Kentaro Miura</td>
      <td>704</td>
    </tr>
    <tr>
      <th>1470</th>
      <td>50 Cápsulas de Amor Propio: Múltiples maneras ...</td>
      <td>1517</td>
      <td>5.0</td>
      <td>32</td>
      <td>16.19</td>
      <td>Personal Transformation</td>
      <td>Perlas para el Alma</td>
      <td>NaN</td>
      <td>Sara Espejo</td>
      <td>228</td>
    </tr>
  </tbody>
</table>
</div>




```python
threshold = df['Review Count'].quantile(0.75) # top 25% most-reviewed books
top = df[df['Review Count'] >= threshold]     # show only books greater than threshold

# sorts 'top' by rating and review count and shows only top 10
top_10 = top.sort_values(by=['Rating', 'Review Count'], ascending=False).head(10) 

# plots top 10 rated books that are within the top 25% most reviewed
sns.barplot(data=top_10, x='Review Count', y='Title', color='thistle')
```




    <Axes: xlabel='Review Count', ylabel='Title'>




    
![png](output_20_1.png)
    


### Genre Analysis 

The top 10 most common genres show that Fantasy has the most book titles with 176 books. This occupies approximately 3.63% of the dataset, which seems rather small considering it is the top genre. However, this makes sense because there seems to be 907 unique genres, as looked at during the inital data exploration. 

When exploring the rating distribution by top genres, a box plot was created. Most genres show median ratings between 4.6 to 4.8, which could indicate that books maintain quality across different genres. The plot shows that Bible have very little variance, with most ratings concentrated between 4.7 to 4.9 reviews. Contemporary and Genre Fiction have the greatest distribution, which makes sense because fiction is a very broad category.


```python
# group by genre and count of titles; gives book count per genre 
genre_count = df.groupby('Genre').agg(book_count=('Title', 'count'))

# sort genre book count and show only top 10 
top_genre = genre_count.sort_values(by='book_count', ascending=False).head(10)

total_books = df.shape[0]

# create new column for genre percentage 
top_genre['Percentage'] = (top_genre['book_count']/total_books).round(4)*100

top_genre
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
      <th>book_count</th>
      <th>Percentage</th>
    </tr>
    <tr>
      <th>Genre</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Fantasy</th>
      <td>176</td>
      <td>3.63</td>
    </tr>
    <tr>
      <th>Classics</th>
      <td>105</td>
      <td>2.17</td>
    </tr>
    <tr>
      <th>Genre Fiction</th>
      <td>101</td>
      <td>2.08</td>
    </tr>
    <tr>
      <th>Motivational</th>
      <td>99</td>
      <td>2.04</td>
    </tr>
    <tr>
      <th>Bibles</th>
      <td>95</td>
      <td>1.96</td>
    </tr>
    <tr>
      <th>Animals</th>
      <td>95</td>
      <td>1.96</td>
    </tr>
    <tr>
      <th>Happiness</th>
      <td>78</td>
      <td>1.61</td>
    </tr>
    <tr>
      <th>Contemporary</th>
      <td>72</td>
      <td>1.49</td>
    </tr>
    <tr>
      <th>Children's Books</th>
      <td>72</td>
      <td>1.49</td>
    </tr>
    <tr>
      <th>Friendship</th>
      <td>66</td>
      <td>1.36</td>
    </tr>
  </tbody>
</table>
</div>




```python
# keeps all books that are part of top 10 genres
df_top = df[df['Genre'].isin(top_genre.index)]

# plot rating distribution by genre
sns.boxplot(data=df_top, x='Rating', y='Genre', color='thistle')
```




    <Axes: xlabel='Rating', ylabel='Genre'>




    
![png](output_23_1.png)
    

