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

### Learnings

- I used cursor chat a lot, it is very convenient to have a chat bar
- Found out about the kagglehub package that can help you interface with kaggle datasets
- Installed langchain and pip install langchain