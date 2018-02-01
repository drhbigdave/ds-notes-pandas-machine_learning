found here:

http://pbpython.com/categorical-encoding.html


excellent way to make a new column of a column with a string in it:
##### Create a binary column called 'recipe_in_title' where it's true if the string 'recipe' is in the title
```
df['recipe_in_title'] = df['title'].str.contains('recipe')
```
awesome way to count nulls in your columns:
```
pd.DataFrame({'dtypes': df.dtypes, 'missing':df.isnull().sum()})
```
**Evaluation of decision trees, from jan 25 class code**
##### Evaluate model on train set
```
print(dt.score(X_train, y_train))
```

##### Evaluate model on test set
```
print(dt.score(X_test, y_test))
```

##### Evaluate model on train set
```
print("Accuracy: %0.3f" % dt_new.score(X_train, y_train))
```

##### Evaluate model on test set
```
print("Accuracy: %0.3f" % dt_new.score(X_test, y_test))
```
##### make a new col with an evaluated temp
```
bikes['is_hot'] = np.where(bikes['temp'] >=80, 1, 0)
```

xml to pandas
http://www.austintaylor.io/lxml/python/pandas/xml/dataframe/2016/07/08/convert-xml-to-pandas-dataframe/

 *replace* method is pretty cool, create a dictionary to indicate the value to be replace (key) and the value to replace it with (value)

##### import wellness single items with timestamp as a dict to compare? or just import with timestamp as index? 
```
pd.read_csv('file.csv' index_col = 'timestamp')
```
##### question - does pokemon.count() and pokemon.value_counts().sum() both equal the same if there are null values?
##### the apply() function will apply a function to a series of data, in section 2 video 42, great explanation of lambda functions, can use to maybe do a pivot table by "if values is in this range, else that range", to count or classify
##### export dynamodb to csv in s3:
https://www.youtube.com/watch?v=MxULtApNYCk
 
 import all csv data from dynamodb, then create new dfs with individual values and particular columns
 
lambda example:
```
ecom['Email'].apply(lambda email: email.split('@')[1])
```

49.95 in google.values 
#####some value in google searches against index: 49.95 in 
#####google.index is the default behavior
```
49.95 in google.values 
```
```
pokemon[ [50:100] ]
pokemon[ [-30: -10] ]
```
extract the index position in a list type behavior

```
google.std()
google.mean()
google.median()
google.sum()
google.mode()
google.max()
google.min()
google.idxmax() #####index where max value is stored
google.idxmin() #####index where min value is stored
google[google.idxmax()] #####does the index corresponding to max and then returns the value
google.value_counts() #####gives a new series and gives an account for how often a values is found. should make a good pivot table
df.nlargest(3, 'column_name') #####returns top 3 values in the chosen column
df.nsmallest() #####same as above but reverse
df['column_name'].nlargest(3) #####return the 3 highest values in that series
```
```
google.apply() ##### apply expects a function in parenthesis
pokemon_names.map(pokemon_types) #####compares first series values to second series (in parenthesis)  index, #####section 2 video 43
pd.read_csv('file.csv').to_dict() #####imports (a series presumably, to a dict)
```

##### DataFrames****

#### EDA and Cleanup
- filter with a comparision operator, then take perform a function/method -  the arithmatic mean of numeric column as per the filter, 
here printing rather than saving anywhere:
```
print(movies[movies.duration < 120].star_rating.mean())
print(movies[movies.duration > 120].star_rating.mean())
```

- change values with map() and replace() and .ix()
```
#change all values at once with map, if a value doesn't meet the criteria, it returns a NaN, not good generally
"data['IsLarge'] = data.Size.map({'small':0, 'large':1})

#to change some values and leave others use replace:
movies.replace(to_replace=['NOT RATED','APPROVED','PASSED','GP'], value='UNRATED', inplace=True)

#from the udemy bond exercise, sect 5 lect 75. 
bond.ix['Dr. No', 'Actor'] = 'Sean Connery' #finds the row for the Dr. No movie w/ Sean C
bond.ix['Dr. No', ['Box Office', 'Budget', 'Actor Salary']] = [448000, 1600, 5000000] #change the values to the ones specified
```


- determine the totals of a categorical column, here content rating

```
movies.content_rating.value_counts().sort_index()
```
- take the totals from the above sort and visualize them:
```
movies.content_rating.value_counts().sort_index().plot(kind='barh', figsize=(15, 5), use_index='True')
plt.ylabel('Movie Rating');
plt.xlabel('Number of Movies');
plt.title('Ratings');
```
```
df.axis #####both df.index and df.columns
df.columns
df.info #####lists unique values per column, will show number of null/non-null
df.get_dtype_counts() #####summary of ##### of columns have which type
df['column with spaces or symbols'] #####so you don't have to rename them, add 2 or more in a list to present a new df in that order

df.sample(n=4, axis = 1) #####returns 3 random cols, cuz axis = 1, default is None/rows
df.insert(3, col = 'new column', value = 'nba') ##### can add new column in particular column index place (3 in example)
df['new column'] = df.['column1'] * .0453592

df.dropna(subset = ['column1']) #####this will remove rows that have a null value in col1
df.fillna(0) #####value is default so this replaces all NaNs with 0
df['column1'].fillna(unk)

df.drop('Row_or_column', axis 0 or 1 or rows or columns)

df.pop() #removes a column, create a variable with it to save it to its own series

del df('column1') #deletes a columns

df.sample() #returns a row(s) at random
```
#2 ways to return a new df filtered on some value
```
mask = df['col1'] == 'some value'
df[mask]
```
#or
```
df.where(mask) #accepts a boolean series, returns all non-True values as Nan
```
```
df.numeric_col.agg(['min', 'max']) #returns the min and max value in the column #eda

df.column_name.unique() #####returns an array of the unique values
len(df.column_name.unique()) #####returns number of unique items
df.colname.nunique() #####returns number of unique values in the specified column, includes dropna = True by default, thus doesn't count null values unless you set it to False

df.column1.astype('int') #####this example changes column type to int, no inplace method so add to df object
df.column1.astype('category') #####if you have many rows and few unique values, changing to category will save significant memory

df.sort_values('Salary', ascending = False, na_position = 'first') #####returns all values, but first ones will be your null values for Salary
df.sort_values(['col1', 'col2'] ascending = [True, False], inplace = True)
df.column.rank() #####rank salaries or the like

pd.to_datetime(df['column_with_strs_for_dates']) #####if df.info() shows date column as strings, mod with pd.to_datetime() or :
df = read_csv('file.csv', parse_dates = ['date_col'])
```

to filter on a value, to leave only the rows, in this case, that are 'male'
```
df['Gender'] == 'Male' #####returns a series of bools
df[df['Gender'] == 'Male'] #####creates a new dataframe with only Male rows
``` 
```
df.drop('column_name', axis=1, inplace=True)
df.drop('row_value_or_numeric_index#####)
df.pop('row_or_col_value) #####removes it but you can save that series or row by creating and object with it; doesn't have inplace but performs it as if it is inplace = True
del df['column_name']
```
##### Filtering and Sorting *** 
- groupby a column, but filter out those that have a count greater less than or equal to 10 in this case:
```
new_df = movies.groupby('genre').filter(lambda x: len(x) >=10) 
#then you can perform actions on that limited df, like getting the mean
new_df.groupby('genre').mean()

#do the same thing without the lambda len function:
top_10 = ['Drama','Comedy','Action','Crime','Biography','Adventure','Animation','Horror','Mystery']
movies[movies['genre'].isin(top_10)].groupby('genre')['star_rating'].mean()
```
- groupby one column and find the highest value in each group 
```
movies.sort_values('star_rating', ascending=False).groupby('genre').title.first()
movies.groupby('genre').title.first()   # equivalent, since DataFrame is already sorted by star rating for imdb dataset
```

```
fnl[fnl['item_name'].str.contains('Chips')] #####str.contains() is cool, try also "startswith"
filtering returns boolean values that let you filter out things you need to.
filtering on 2 conditions, can do a range with this, i.e. date range:
mask = df['Gender'] == 'Male'
mask2 = df['Team'] == 'Marketing'
df[mask & mask2]
mask = df['column'].isin(['value1', 'value2', 'value3']) to filter on several values, can compare to series from another dataframe
df[mask]
```

##### filter on the nulls:
```
mask = df['column'].isnull() #####complimentary method is notnull()
df[mask]
```
##### filter on a range:
```
df['column'].between(first_value, second_value)
```
```
df.between() #####seems to not work on hour parameter arguments only
df.between_time() ##### so i set the index to 'Datetime' and used between_time(), if Datetime isn't the index you get a DatetimeIndex error
```
```
df.['column_name'].duplicated() #####returns the duplicates, does not return the first or last occurrence (if you choose first or last)
```
##### if you want to return the first duplicate values:
```
~df.['column_name'].duplicated(keep=False) #####the tilde reverses the filter, makes the falses to trues, which in this case returns the first instance, this will return a series of bools, apply to a variable and see the first occurrence of the value
```
##### to find those values that are unique, that have no dupes:
```
df.drop_duplicates(keep = False) #####keep parameter can accept first and last also
```
##### Index stuff***
get location with index or slice
```
pandas.Index.get_loc
```
```
df.set_index('desired_col_for_index') #####sort_values afterward is best practice
```
can also set index with:
```
df = pd.read_csv('filename.csv', index_col = 'desired_column')
df.reset_index() #####sets it back to 
```
##### .loc[], .iloc[], .ix[]
```
df.loc[] #####must use square brackets on this method; will return a row, or will return a single entry as a new series with the row columns being turned into index labels

df.loc['some_column' : 'another_column'] #####returns that range, inclusively, as it returns the last value

df.iloc[0] #####returns a row based on its numeric index #####; if you set your index to a non-numeric index, there is a still an unseen default numeric index you can use

df.ix[] can mix and match numeric index or label 
```

##### you can return single values, much like a search, for this example, you can have a custom non-numeric index, and return the particular value from the column you want:
```
df.loc['name_of_an-index_postion', 'occupation'] #####would return the value of the occupation column in the name you found
```
##### read_csv for tsv or others:
https://stackoverflow.com/questions/45551324/dynamodb-pipe-object-to-pandas-dataframe

### Visualizations
- pandas plot is ambiguous at times, this example you can see a bit of a relationship, but mostly a blob:
```
movies.plot(kind='scatter', x='duration', y='star_rating',figsize=(10, 6))
```
- seaborn gives you a nice regression line if you want:
```
sns.regplot(x=movies['duration'], y=movies['star_rating'])

sns.regplot(x=df["sepal_length"], y=df["sepal_width"], fit_reg=False) #without regression fit

```



- simple histogram with 1 dimension, shows the distribution:

```
movies.duration.plot(kind='hist', figsize=(15, 5), bins=50)
plt.xlabel('duration');
plt.ylabel('minutes');
plt.title('Duration');
```

- same data, but with boxplot:
```
movies.duration.plot(kind='box', figsize=(15, 5))
plt.xlabel('duration');
plt.ylabel('minutes');
plt.title('Duration');
```
https://python-graph-gallery.com/

Pandas S13L169

change high stock price to category:

```
def custom_round(stock_price):
    return int(stock_price / 100) * 100 #int removes decimal, makes anything less than 100 = 0, 100 - 199 = 100 and so on

 df['high'].apply(custom_round).value_counts().sort_index() 

df['high'].apply(custom_round).nunique() #take this unique value and use it for the # of bins

df['high'].apply(custom_round).plot(kind = 'hist', bins = 9)

```






