## Writeup for project
### Zhengqian Xu

### Introduction
In this project, I explore, assess and visualize the reddit data. I summarize the data to get a general idea and find out suitable variables that I can use in the model. And finally I decide to use 4 predictors in my model, which are subreddit_type, controversiality, no_follow and collapsed to predict score. Then I transform them into integer or numeric for further usage. Based on the type of transformed variables, I choose to use the NaiveBayes and random forest to build the model, and compute the accuracy for each model.

### Code
0430.ipynb

### Methods section
First, I combine the four datasets and take a summary of them. After I use dtypes to check the type of each column, I see most of columns are unuseful. Now, in order to analyze the data further, I do some visualization. I use groupby and count to see the table of qualitative variables as subreddit_type, stickied. And I also use seaborn to plot the distribution of continous variables as score, which would be used as my response. 

Since many columns are in string format and cannot be used to build model, I need to select suitable features from them. After checking the data, I find that **subreddit_type** is a good string-format column which I can utilize. Also, **no_follow** and **collapsed** are two good boolean-format columns. **controversiality** is the int-format column I will use. And I choose **score** as my response to predict. Since **score** ranges large, I partition it into 4 groups through sql, named as **score_bin**. Now, I need to convert all string fields -**subreddit_type, score_bin**- to numeric ones through StringIndexer transformer. Then I transform boolean columns into integer format. Now, I have 4 predictors, which are subreddit_si:int, controversiality:int, no_follow:int and collapsed:int. I use them to predict **score_bin_si**.  

I use NaiveBayes and random forest to model the data. Since I need to predict for score_bin_si, which has 4 labels, logistic regresion is not a good choice. Moreover, all my predictors have discrete distribution, either boolean or integtger after transformation, so it would be great to use Naivebayes to build model. Random forest is also a good model for discrete predictors. I use the VectorAssembler to merge selected columns into a single vector column and randomly split data into train data (70%) and test data(30%). Train data helps to build model. Then I use this model to make predictions on test data so I can measure the accuracy of the model on new data.

### Results section
For the exploratory part, let me summarize the result. Subreddit_type stands for the type of subreddit, and most of them belong to public while a small amount belong to restricted. For no_follow column, a quarter of population has followers. Most posts are controversial according to the graph. Last, score means the popularity of a post, which ranges from negative to 20 thousand. It shows that for a specific post, people tend to have various attitude towards it. I believe the subreddit_type, whether the post is controversial, whether having followers will all affect the score, so I build the model to predict the score_bin.  

As we can see, for NaiveBayes Model, the accuracy for test data is 0.72. For random forest model, the accuracy for test data is 0.82. Since random forest makes decision based on many trees, it will definitely performs better than the NaiveBayes model. Both of them prove to be good model, these four predictors indeed decides the score to some extent.

### Future work
If I redo the project in the future, I will explore more variables and add more attributes into my model. Maybe I will take a look at other qualitative variables such as is_submitter, which might increase the accuracy of my model. Also, since there are some columns contains text- comments and text, do NLP models like LDA may also tell an interesting story. For example, collapsed_reason tells us the reason why users want to collapse their account, which can help developer to improve the community.
