Dataset - 7k books (https://www.kaggle.com/datasets/dylanjcastillo/7k-books-with-metadata)

In this project we are going to 

1. Prepare text data
2. Vector Search
3. Text Classification
4. Sentiment Analysis
5. Gradio dashboard


Potentially create a react frontend

### The process and tools
- langchain, langchain-openai, langchain chroma
- chroma - vectordb
- transformers hugging face
- gradio 
- ipywidgets

#### Data Exploration

started data exploration in a jupyter notebook file. We installed the kagglehub package to allow us to download the dataset automatically from Kaggle. 

![Screenshot of Data Exploration](/images/kaggle-d.png)

looked at the dataset to get a sense of what is in there. Since this is a sematic recommender system, we immediately notice that the description colum would be important. We see that all the books are unique so there would be no deduplication 

![Data summary](./images/data%20stats.png)

- Spent a lot of time on data exploration to make sure the data we use to feed this recommender system is meaningful. This exploration phase included looking at what columns had missing values, looking into those columns and deciding if we need to do something to enahnce the semantic meaning of the data or if it was too noisy or random that we would not include it in the system.

Also in the description column, we see that some books descriptions are not very long. This could be a problem for the semantic meaning of the data. We will need to do something about this. When we looked at the distribution of the desceiption column we find that we have an even distribution so there was no natural break point for the description length. So we had to decide a breakpoint ourselves. After doing some digging into the column we decided about 25 words was a good breakpoint.

Since the substitle column did not have a lot of data, the column iteself is not that useful. So we decided to create a new columns and append those that have a subtitle to the parent title since that information is part of the book name.

At the end we dropped the columns we did not need and saved the cleaned dataset into a csv file.

#### Turning raw Text into a vector and Creating a vector database

This allows us to capture the meaning of the text and allows us to compare how simsimilar or different pieces of text are.

Next, we store this processed data in a special type of database called a "vector database." Each book is represented as a list of numbers, called a vector, that captures the meaning of its description. When we want to find books similar to a user's query, we convert the query into a vector and search the database for vectors that are close to it. This approach uses a technique called "embeddings," which is also used in large language models (LLMs) to find and compare similar pieces of text. This way, the recommender system can suggest books that are semantically similar to what the user is looking for, even if the exact words aren't used.

How this works is it represents the text in a three dimensional space. Each word is a point in this space. The distance between two points is the similarity between the two words. The closer the points are the more similar the words are. This is a way to capture the meaning of the text and allows us to compare how semantically similar or different pieces of text are. The value for each word across this hypothetical graph are word embeddings. They define the meaning of a word by grouping words that are similar and creating distance between words that are not similar.

We use a word embedding model. The main issue with earlier word embedding models like word2vec is that they give a word a fixed vector value. This means that the understnading of the word does not pay attention to the context of the word. This is where the latest generation of models (transformer models) solve this problem by giving the vectors a positional vectors to indicate where the word is in a sentence which allows the model to understand the context of the word by using the models attention mechanism to understand the meaning of the word in the context of the sentence. The attention mechanism uses the information from the postition vector weighted embeddigns to let it know how to allocate its attention to the other words in the sentence to get the semantic meaning of the word.

#### Langchain

Langchain is a framework for building applications that use language models. We are going to use it for vector search

Had to get an OpenAI API key to use the OpenAIEmbeddings model and a hugging face API key to use the HuggingFaceEmbeddings model.

We first split the text into document chunks. This prepares the books for semantic vector search. It does this by taking a text file of the descriptions and splitting them into smaller chunks of text.

The `TextLoader` tool in Langchain helps you easily load and read text files so you can process the content in your application. The `CharacterTextSplitter` (character split) tool is used to break up large blocks of text into smaller, manageable chunks or pieces based on a character limit you set. This makes it easier to process long text by working with smaller parts at a time, which is useful for things like searching, embedding, or summarizing text.

We then chreate a Chroma vector database and store the document chunks embeddings in it. Chroma is the vector DB and we use langchains OPENAI EMBEDDINGS to create the embeddings.

```python
db_books = Chroma.from_documents(docs, embedding=OpenAIEmbeddings())
```

We can then use the `similarity_search` method from the vector database to find the most similar books to a given query.

```python
query = 'What are the best history books?'
query_docs = db_books.similarity_search(query, k=10)
query_docs
```

This will return the top 10 most similar books to the query.


### Learnings

- I used cursor chat a lot, it is very convenient to have a chat bar
- Found out about the kagglehub package that can help you interface with kaggle datasets
- Installed langchain and pip install langchain