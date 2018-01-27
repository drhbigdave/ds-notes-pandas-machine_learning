## Python supporting methods/functions, to include Numpy

"list comprehension"
```
x = [1,2,3,4]
new_list = [num_var**2 for num_var in x]
```
creates new list
[1, 2, 9, 16]

filter like map, but rather than perform an operation or function on each item in a list, you can filter out stuff.

map example, with lambda function, and creating a list you can see the result:
```
list(map(lambda num : num**2, seq) #seq being a list declared earlier of [1, 2, 3]
```
[1, 4, 9]
```
list(filter(lambda num: num%2 == 0, seq)
```
[2]
-returns the even values

- split method splits on whitespace by default, or pass in a different parameter to split on:


from __future__ import division
from __future__ import print_function

http://python-future.org/compatible_idioms.html

itertools - for iterables , lots of tools

lists
```
nums = range(1, 30, 2)
num.pop() - empty acts on end, otherwise supply index
```
removes 29
```
nums.insert(3, 7) # index and value
nums.append(31)
nums.remove(31)
nums[4] # returns index #4 value

to increment the value 1
```
found['e'] = += 1
```
------------------------------------------------------------------------------------
#### Anaconda

create virtual environments:
```
conda create my_env_name python pip sqlalchemy
```
- there must be at least 1 package with the create
```
source activate my_env_name
```
- to start the virt env on mac


https://www.activestate.com/blog/2017/05/pandas-framing-data

grab the csv's from athena work and try doing the commands here? 

**kwargs - key worded variable length argument list
*args - non key worded variable length argument list

"That’s a great question. On the face of things, you don’t know. However, there’s a well-established convention in the Python programming community to name functions using lowercase letters (with underscores for emphasis), while CamelCase (concatenated words, capitalized) is used to name classes. Following this convention, it should be clear that count_from_by() is a function call, whereas CountFromBy() creates an object. All is fine just so long as everyone follows this convention, and you’re strongly encouraged to do so, too. However, if you ignore this suggestion, all bets are off, and most Python programmers will likely avoid you and your code."
