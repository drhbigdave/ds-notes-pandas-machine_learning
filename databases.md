####Database interactions with Pandas and Python
-Notebooks
sql-and-pandas.ipynb - GA
solution-code-17.ipynb -GA
*go look at Activity:Extra SQL Practice in the slide deck


normalized vs denormalized tables : smaller tables vs bigger, smaller lesser perf impact on system, bigger are simpler

shows all the tables available:
```
sql.read_sql('SELECT * FROM sqlite_master', connection)
```

create a function to do queries with:
```
# In the case that typing out sql.read_sql() is a little too much,
# we'll create a function shortcut.


CARS = sqlite3.connect('../data/sql/Cars.db.sqlite')


def Q(query, db=CARS):
    return sql.read_sql(query, db)
```

insert 
```
new_car = (None, 'Ferrari','The Ferrari')
CARS.execute('INSERT INTO car_names VALUES (?, ?, ?)',new_car)
CARS.commit()
```
# Select the store, date and fuel price on days it was over 90 degrees
query = """
SELECT 
Date, Store, Fuel_Price, Temperature
FROM walmart_features
WHERE Temperature > 90
"""
sql.read_sql(query, con = conn).head()
