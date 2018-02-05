### Natural Languare Processing
NLP Notebooks:
*NLP drh v2.ipynb
*NLP (Natural Language Processing) with Python.ipynb - has a lot of explanation of the process
*add notebooks from GA

- if you use the nltk shell with ```nltd.shell_downloader() ``` you must remember to 'q' quit or your subsequent work will hang.

#### Step 1 EDA or Text Pre-Processing
-bring in data, do some initial visualizations, in the Udemy ML class we find message length on text messages seem a promising feature

- *Now we must vectorize the text/string data so the classification algorithms we have have a numerical feature vector to work with
- *Must create/transform the text to vector format, here we will use "bag of words"

- Tokenize = the process where we take strings of text into tokens, removing the punctuation and extraneous words
- remove punctuation with the string function
```
import string
#remove punctuation
nopunc = [c for c in mess if c not in string.punctuation]

#import stopwords, presumably possible since we did it once with nltk.shell_download() previously on this machine
from nltk.corpus import stopwords

#we spent a good bit of work in NLP drh v2.ipynb learning how to remove punctuation and extra words, lemmitization, ultimately creating this function:
def process_text(message):
    '''
    remove punc, join back up, remove stopwords
    '''
    nopunc = [char for char in message if char not in string.punctuation]
    
    nopunc = ''.join(nopunc)
    
    return [word for word in nopunc.split() if word.lower() not in stopwords.words('english')]

```

#### Vectorizing

##### lemmitizing and removing punctuation in a bag of words vector

```
from sklearn.feature_extraction.text import CountVectorizer 
bow_transformer = CountVectorizer(analyzer=process_text).fit(df['messages'])

#a quick look at the word matrix on a single column:

mess4 = df['messages'][4] #5th index value
bow4 = bow_transformer.transform([mess4])
print(bow4)
#use the printed indices to see the word
bow_transformer.get_feature_names()[2948]


#transform entire corpus
messages_bow = bow_transformer.transform(df['messages'])

type(messages_bow) #returns scipy.sparse.csr.csr_matrix

messages_bow.nnz # returns number of nonzeros

#examine the sparsity, the number of nonzeros as they relate to the total:

sparsity = (100.0 * messages_bow.nnz / (messages_bow.shape[0] * messages_bow.shape[1]))
print('sparsity: {}'.format(sparsity))

```
##### TF-IDF

"The importance increases proportionally to the number of times a word appears in the document but is offset by the frequency of the word in the corpus."
```
from sklearn.feature_extraction.text import TfidfTransformer

tfidf_transformer = TfidfTransformer().fit(messages_bow) # instantiate

#try the idf transformer on 1 row
tdidf4 = tfidf_transformer.transform(bow4)
print(tdidf4)

#weighted value of some word in the corpus?
tfidf_transformer.idf_[bow_transformer.vocabulary_['university']]

#now pass in whole bow
messages_tfidf = tfidf_transformer.transform(messages_bow)
```

- now we can choose a classifier and begin predicting
```
#create our model:
spam_detect_model = MultinomialNB().fit(messages_tfidf,df['label'])

#check against 1 message
spam_detect_model.predict(tdidf4)[0] #returns spam or ham, subsequently checking against df['label'][4] validates
```

- that was how it is learned, this is how it is done, with a pipeline, also below we must do it again as in the learning steps we did not split the data up into
train and test data.

```
from sklearn.cross_validation import train_test_split
from sklearn.pipeline import Pipeline

#THIS * pipeline, useful for re-doing or repeating 

pipeline = Pipeline([
    ('bow',CountVectorizer(analyzer=process_text)),
    ('tfidf', TfidfTransformer()),
    ('classifier',MultinomialNB())
])

#now split
msg_train, msg_test, label_train, label_test = train_test_split(df['messages'],df['label'], test_size=0.3)

#now fit

pipeline.fit(msg_train,label_train)

#now predict

predictions = pipeline.predict(msg_test)

#now evaluate

from sklearn.metrics import confusion_matrix,classification_report
print(classification_report(label_test, predictions))

#now checkout a different classifier/model/algo

from sklearn.ensemble import RandomForestClassifier

pipeline = Pipeline([
    ('bow',CountVectorizer(analyzer=process_text)),
    ('tfidf', TfidfTransformer()),
    ('classifier',RandomForestClassifier())
])

pipeline.fit(msg_train,label_train)

predictions = pipeline.predict(label_test, predictions)

print(classification_report(label_test, predictions))






