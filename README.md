# Twitter Sentiment Analysis Project

This project focuses on training a Naive Bayes model to predict whether a tweet carries a positive or negative sentiment. The project simulates Twitter's streaming data, as Twitter (now known as X) ceased offering a free API from June 2023. The simulation is achieved by sequentially reading lines from a stored file.

## DataSet

The dataset used is the [Sentiment140 dataset from Kaggle](https://www.kaggle.com/datasets/kazanova/sentiment140), featuring 1.6 million labeled tweets.

## Files in the Project

### `twitter_sentiment_nb_train.ipynb`

This Jupyter notebook is primarily for data processing and pipeline creation. It covers the following steps:

1. **Download and Explore Data**
2. **Data Cleaning and Target Variable Transformation**
3. **Save the Pipeline of Transformation**
4. **Define and Fit a Machine Learning Pipeline**
5. **Save the Model and Test the Saved Model**
6. **Next Step**

### `simulate_streaming.ipynb`

This notebook simulates the streaming of data. It sequentially reads each line from the file `training.1600000.processed.noemoticon.csv`, which is stored as `review{}.txt` in the `/databricks/driver/tmp/` directory.

### `Streaming_Tweet_Sentiment_Prediction.ipynb`

Run this notebook after starting `simulate_streaming.ipynb`. It performs the following operations:

1. **Load Saved Data Transformation Pipeline**: The `fitted_target_pipeline` is used to format the streaming data for prediction.
2. **Load Saved Pipeline Model**: The `pipelineModel` applies the model to the streaming data.
3. **Data Transformation**: Transform the streaming data into the appropriate format for prediction.
4. **Cleanup Output**: Remove intermediate columns, retaining only the text, time, and prediction in the final output.
5. **Output to Memory Sink**: The results are sent to a memory sink (`scored_tweets`) in append mode, with output triggered at 2-second intervals.

Finally, use SQL queries to view the streaming results and observe the count of positive and negative sentiments in the streaming data.

