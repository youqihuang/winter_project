<b>Name:</b> Youqi Huang, <b>Email:</b> youqihua@usc.edu

<b>Project Description:</b> I choose the news headline sarcasm detection task. The dataset included headlines from Huffington Post and the Onion articles, and I used a pre-trained transformer model to classify the headlines are sarcastic or not. 

<b>Dataset:</b> I downloaded "News Headlines Dataset For Sarcasm Detection" dataset from Kaggle and choose to drop the urls for each article. In the curriculum project I did last semester, I worked on a similar task (detecting fake news based off headlines and body text). We choose to drop the urls in that task as well, because the name of the publication is present in each url and a model may use the publication's name as a heuristic to determine the sarcasm of the headline instead of the headline itself. \
I also balanced the subsamples to make sure there was an equal amount of saracastic and non-sarcastic cases. Having a balanced subsample helps make sure there is no majority class. In curriculum, we discussed that in the presence of an extremely large majority class that takes up 98% of the data, for example, a model could predict the majority class in all cases (therefore, not <i>actually</i> learning the task) and still achieve high accuracy. \
In consideration of the computing resources I had access to, I also had to drop data. I selected 2000 data points to begin with and was left with 1306 data points for trainig and 644 data points for testing after balancing the subsample and utilizing a 67-33% train-validation split. 

<b>Model Development and Training</b>: I used a pre-trained Sentence BERT model, as well as the tokenizer it came with. Sentence BERT is additionally fine-tuned for sentence classication, so I decided to use this instead of a classic BERT model. I trained for 5 epochs, using a batch size of 8 and a learning rate of 1e-4. I tried different batch sizes (8, 16, 32), learning rates (1e-3, 1e-4, 1e-5) as well as the number of epochs I trained for (5, 10) before reaching my current setup. 

<b>Model Evaluation and Results</b>: I used the sci-kit learn classifcation report to generate values for precision, recall, accuracy and f1-score, which I will list below. 

|              | Precision | Recall | F1-Score | Support |
| -----------:  | :-------: | :----: | :------: | :-----:
|       0      | 0.89      | 0.91   | 0.90     | 320
|       1      | 0.91      | 0.89   | 0.90     | 324
|   Accuracy   |           |        | 0.90     | 644
|   Macro Avg  | 0.90      | 0.90   | 0.90     | 644                    
| Weighted Avg | 0.90      | 0.90   | 0.90     | 644

<b>Discussion: </b> I observe some room for improvement across all metrics. In theory, Sentence BERT should perform better than a standard BERT model like RoBERTa and I also validated this empirically with a few short experiments before I settled on Sentence BERT. This leaves me to believe that the model could be improved through further refining my training procedures, specifically the hyperparameters I've chosen for the task. I could also use grid search to perform a more extensive survey of possible hyperparameter combinations. Though there are not many features in the dataset, the task of binary classifcation is fairly simple so this should not be the reason my model is not performing well. \
The task of sarcasm detection may not seem immediately applicable to social good, but the task of tone reading can have important implications. People who have autism may struggle with sarcasm, or recognizing tone indication both written or spoken communication. A classifier that can help mark tweets on social media as sarcastic or serious, may be helpful for these people as right now users must consciously tag their tweets with indicators like "/s" or "/j" for their audience, and many do not tag their tweets at all. \
A limitation in my current method may be the type of data the model would be trained on. Tweets are longer and are written with different syntax and grammar than headlines, so it may be helpful to train the model directly on a dataset of tweets, especially when you consider that there are so many freely avaiable or the ease in which you can crawl your own. \
To continue this project, my next steps would be to first pivot to a different dataset more suited for the adapted task at hand, then focus on achieving a near-perfect accuracy, as it should be possible for a binary classifcation task like this. I then might expand to a multi-class problem of recognizing different tones, like hyberbole or rhetorical questions. Finally, this could be deployed as a web tool like a browser extension that could modify a user's Twitter feed as they scroll through it. 
