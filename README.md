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

### Learnings

- I used cursor chat a lot, it is very convenient to have a chat bar
- Found out about the kagglehub package that can help you interface with kaggle datasets
- Installed langchain and pip install langchain