---

---


# Model Card for Go Phish

<!-- Provide a quick summary of what the model is/does. [Optional] -->
The goal of this model is to classify emails as either legitimate (ham) or phishing scams (spam). The model uses the emails gathered in the Enron data set and relies on word embeddings and LSTM cells. 




#  Table of Contents

- [Model Card for Go Phish](#model-card-for--model_id-)
- [Table of Contents](#table-of-contents)
- [Table of Contents](#table-of-contents-1)
- [Model Details](#model-details)
  - [Model Description](#model-description)
- [Uses](#uses)
  - [Direct Use](#direct-use)
  - [Downstream Use [Optional]](#downstream-use-optional)
  - [Out-of-Scope Use](#out-of-scope-use)
- [Bias, Risks, and Limitations](#bias-risks-and-limitations)
  - [Recommendations](#recommendations)
- [Training Details](#training-details)
  - [Training Data](#training-data)
  - [Training Procedure](#training-procedure)
    - [Preprocessing](#preprocessing)
    - [Speeds, Sizes, Times](#speeds-sizes-times)
- [Evaluation](#evaluation)
  - [Testing Data, Factors & Metrics](#testing-data-factors--metrics)
    - [Testing Data](#testing-data)
    - [Factors](#factors)
    - [Metrics](#metrics)
  - [Results](#results)
- [Model Examination](#model-examination)
- [Environmental Impact](#environmental-impact)
- [Technical Specifications [optional]](#technical-specifications-optional)
  - [Model Architecture and Objective](#model-architecture-and-objective)
  - [Compute Infrastructure](#compute-infrastructure)
    - [Hardware](#hardware)
    - [Software](#software)
- [Citation](#citation)
- [Glossary [optional]](#glossary-optional)
- [More Information [optional]](#more-information-optional)
- [Model Card Authors [optional]](#model-card-authors-optional)
- [Model Card Contact](#model-card-contact)
- [How to Get Started with the Model](#how-to-get-started-with-the-model)


# Model Details

## Model Description

<!-- Provide a longer summary of what this model is/does. -->
The goal of this model is to classify emails as either legitimate (ham) or phishing scams (spam). The model uses the emails gathered in the Enron data set and relies on word embeddings and LSTM cells. 

- **Developed by: Grant Martin and Misbah Imtiaz
- **Model type:** Language model
- **Language(s) (NLP):** english
- **License:** N/A
- **Parent Model: N/A
- **Resources for more information:** 
    - [GitHub Repo](https://github.com/Grantmartin2002/GoPhish)


# Uses

## Direct Use

The model is intended to be used only on the Enron data set for now to illustrate a proof of concept. For future use, we hope to train the model of more data sets of spam and ham emails to that the model can be used on modern day emails. 


# Bias, Risks, and Limitations

This model is only trained on emails found in the Enron data set. This introduces bias as the emails were sent amongst employees and may not captivate other types of emails being sent today. Additionally, since the data set is from the early 2000s, it doesn't account for the recent upsurge in new spam emails which could mean the model will not perform as well on new data.  


## Recommendations

For future use, we should look to find new data set to train the model on to reduce the bias and inrease accuracy with modern emails. 



# Training Details

## Training Data

Extracted from our own research article: 

The data set we have chosen is known as the Enron Data set. There were 600,000 emails from the company gathered and publicly released by the by the CALO Project (A Cognitive Assistant that Learns and Organizes) [3]. In 2006, a paper was published by Metsis, Androutsopoulos, and Paliouras at the third conference on email and anti-spam that took the original data and combined a mixture of faulty (spam) and legitimate (ham) emails [1]. This data set can be found here: \href{https://www2.aueb.gr/users/ion/data/enron-spam/}{https://www2.aueb.gr/users/ion/data/enron-spam/}. From this newly infused data set, we used 16545 ham and 17171 spam pre-processed emails. The email samples itself are each stored in their own text file including the subject, body, and other general header information such as who the email is being sent to and where its coming from.


## Training Procedure
The email classification model was trained using the Adam optimizer with a learning rate of 0.001 and the binary cross-entropy loss function was used as the objective function. To improve the model's performance, we incorporated a learning rate scheduler with a patience of 2 and a factor of 0.5, meaning it halves the learning rate when the validation loss stops improving for 2 epochs.

The hyperparameters used in the model include a hidden size of 128 an LSTM layer count of 2. The model was trained for 20 epochs on the training set with a batch size of 64, and we monitored the validation loss at the end of each epoch. To track the model's performance, we recorded the training and validation losses for each epoch and printed the average train and validation loss.

### Preprocessing

Extracted from our own research article:

Firstly, the dataset was truncated to a maximum email length of 200 words, and the number of emails in each category (spam and ham) was balanced to avoid class imbalance during training. Specifically, emails were randomly sampled from each category to create a new dataset with an equal number of emails in each category. The resulting dataset was a list of emails and corresponding labels, where each label indicated whether the email was spam or ham.

Next, the email texts were tokenized, meaning that each word was converted to a unique index. This process was performed using a dictionary to map each unique word to an index, and each email was converted to a sequence of indices representing the words in the email. The sequences were then padded to be of equal length, which is necessary for input into the LSTM layers of the model.

Finally, the labels were converted to categorical format, where each label was assigned a unique integer value. The preprocessed dataset was split into training, validation, and test sets, with a split ratio of 60\%, 20\%, and 20\%, respectively. The data was then loaded into PyTorch data loaders with a batch size of 64 for efficient training.

In summary, the data preprocessing steps included truncating and balancing the dataset, tokenizing and padding the email sequences, converting labels to categorical format, and splitting the dataset into training, validation, and test sets.

### Speeds, Sizes, Times

Use a NVIDIA GPU with cuda tool kit otherwise running a single epoch will take hours compared to a couple of minutes. 

 
# Evaluation

 We evaluated the model using Accuracy, Precion, Recall, F1 score, and ROC-AUC score. 

## Testing Data, Factors & Metrics

### Testing Data
we used 20% of the Enron dataset for testing.  



## Results 

### Metrics

Our model achieved an accuracy of 98.37\% with a precision and recall metric of 98.51\% and 98.22\% respectively. Our F1 score is 98.37\%. Furthermore, we had an AOC-ROC score of 99.63\%. The high ROC-AUC score indicates that the model is able to distinguish between the two classes very well. 

# Environmental Impact

<!-- Total emissions (in grams of CO2eq) and additional considerations, such as electricity usage, go here. Edit the suggested text below accordingly -->

Carbon emissions can be estimated using the [Machine Learning Impact calculator](https://mlco2.github.io/impact#compute) presented in [Lacoste et al. (2019)](https://arxiv.org/abs/1910.09700).

- **Hardware Type:** NVIDIA GTX 1080TI
- **Hours used:** N/A
- **Cloud Provider:** N/A
- **Compute Region:** N/A
- **Carbon Emitted:** N/A

# Citation

[1] Androutsopoulos, I., Koutsias, J., Chandrinos, K. V., Paliouras, G., & Spyropoulos, C. D. (2006). Spam filtering with naive Bayes - Which naive Bayes? Proceedings of the 3rd Conference on Email and Anti-Spam (CEAS), Mountain View, CA, USA, 26-27 July 2006, 17-28.

[2] Cohen, W. (2015, May 8). Enron Email Dataset. Enron email dataset. Retrieved April 25, 2023, from https://www.cs.cmu.edu/~enron/ 

[3] Enron Corp & Cohen, W. W. (2015) Enron Email Dataset. United States Federal Energy Regulatory Commissioniler, comp [Philadelphia, PA: William W. Cohen, MLD, CMU] [Software, E-Resource] Retrieved from the Library of Congress, https://www.loc.gov/item/2018487913/.

[4] Editor, C. S. R. C. C. (n.d.). Phishing - glossary: CSRC. CSRC Content Editor. Retrieved April 24, 2023, from https://csrc.nist.gov/glossary/term/phishing 

[5] James, N. (2023, April 5). Phishing statistics and DMARC. EasyDMARC. Retrieved April 25, 2023, from https://easydmarc.com/blog/phishing-statistics-easydmarc-report-january-june-2022/\#:~:text=Globally%2C%2096%25%20of%20phishing%20attacks,phone%20(vishing%20and%20smishing). 

[6] The latest phishing statistics (updated April 2023): Aag it support. AAG IT Services. (2023, April 13). Retrieved April 25, 2023, from https://aag-it.com/the-latest-phishing-statistics/\#:~:text=The%20US%2Dbased%20IC3%20received,phishing%20and%20zero%2Dday%20attacks 


# How to Get Started with the Model

Use the code below to get started with the model.

<details>
<summary> Click to expand </summary>

git clone git@github.com:Grantmartin2002/GoPhish.git
run each cell

</details>
