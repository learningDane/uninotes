#uni 
NLP: Natural Language Processing

# Tokenization
```python
import nltk
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
from nltk.stem import PorterStemmer
```
# Bag of Words - BoW
Represents text as a vector of word frequencies.

Limitations:
- loses word order
- ignores semantics
- large, sparse vectors
- give high importance to common words

```python
from sklearn.feature_extraction.text import CountVectorizer
```
# Term Frequency-Inverse Document Frequency - TF-IDF
Like BoW but down-weights common words.
- TF: term frequency in a document
- IDF: inverse document frequency: log of docs containing the word
```python
from sklearn.feature_extraction.text import TfidfVectorizer
```
# Word Embeddings
Mapping words to dense vectors in a continuous vector space, capturing semantic relationships.

Popular embeddings:
- Word2Vec
- GloVe
- FastText
# Transformer Architecture
[[Attention is all you need]], one of the most famous papers of all time.
# Hugging Face
```python
from transformers import BertTokenizer, BertModel
```
# Large Language Models

Transformer based model with strong NLP capabilities, large bceause they have billions of parameters.

An LLM is trained in 3 steps: pretraining, finetuning and preference tuning.
## LaaJ - LLM as a Judge