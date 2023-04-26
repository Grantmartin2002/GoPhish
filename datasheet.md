# Data Sheet for Go Phish
## Data Source: 
Preprocessed Enron Data Set from ( https://www2.aueb.gr/users/ion/data/enron-spam/)

## Data Format: 
Series of files and folders of text files labeled with spam and ham. 

## Data Size: 
16545 ham and 17171 spam preprocessed emails

Email lengths used range from 1 word to 37,138 words


## Data Preprocessing and Labeling:
Firstly, the dataset was truncated to a maximum email length of 200 words, and the number of emails in each category (spam and ham) was balanced to avoid class imbalance during training. Specifically, emails were randomly sampled from each category to create a new dataset with an equal number of emails in each category. The resulting dataset was a list of emails and corresponding labels, where each label indicated whether the email was spam or ham.

Next, the email texts were tokenized, meaning that each word was converted to a unique index. This process was performed using a dictionary to map each unique word to an index, and each email was converted to a sequence of indices representing the words in the email. The sequences were then padded to be of equal length, which is necessary for input into the LSTM layers of the model.

Finally, the labels were converted to categorical format, where each label was assigned a unique integer value. The preprocessed dataset was split into training, validation, and test sets, with a split ratio of 60\%, 20\%, and 20\%, respectively. The data was then loaded into PyTorch data loaders with a batch size of 64 for efficient training.

In summary, the data preprocessing steps included truncating and balancing the dataset, tokenizing and padding the email sequences, converting labels to categorical format, and splitting the dataset into training, validation, and test sets.


## Data Splits:
Used a 60-20-20 split for training, validation, and test sets, respectively

