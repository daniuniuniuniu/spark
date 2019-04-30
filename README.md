## Writeup for project
### Zhengqian Xu

### Introduction

### Methods section
How you cleaned, prepared the dataset with samples of intermediate data
Tools you used for analyzing the dataset and the justification (tools, models, etc.)
How you modeled the dataset, what techniques did you use and why?
Did you have a hypothesis that you were tryig to prove?
Or did you just visualize the dataset?

Since many columns are in string format and cannot be used to build model, I need to select suitable features from them. After checking the data, I find that **subreddit_type** is a good string-format column which I can utilize. Also, **no_follow** and **collapsed** are two good boolean-format columns. **controversiality** is the int-format column I will use. And I choose **score** as my response to predict. Since **score** ranges large, I partition it into 4 groups through sql, named as **score_bin**. Now, I need to convert all string fields -**subreddit_type, score_bin**- to numeric ones through StringIndexer transformer. Then  I transform boolean columns into int format.
Now, I have 4 predictors, which are subreddit_si:int, controversiality:int, no_follow:int and collapsed:int. I use them to predict **score_bin_si**.

I use groupby to see distribution of qualitative variables as subreddit_type, no_follow. And I also use seaborn to plot the distribution of continous variables as score.

I use NaiveBayes and random forest to model the data. Since I need to predict for score_bin_si, which has 4 labels. It is a multi-classification. Moreover, all my predictors have discrete distribution, either boolean or integtger after transformation, so it would be great to use Naivebayes to build model. Random forest is also a good model for discrete predictors.

### Results section


### Future work
