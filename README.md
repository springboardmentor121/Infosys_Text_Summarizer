# INFOSYS SPRINGBOARD INTERNSHIP 2024 
## A Report On Text Summarizer Model
### Initial Design for the Project Work:

![Initial Design Image](<Initial Design Image.png>)

# Text Summarizer
### Abstract:
<p align="justify"> This project, developed as the part of Infosys Springboard internship, focuses on creating a Text Summarizer using Natural Language Processing(NLP) techniques. The summarizer aims to reduce the length of documents while preserving key information and meaning, making it easier for users to quickly understand the content of large texts.</p>

### Objectives:
- Develop an automatic text summarization tool [Both Extractive and Abstractive] using NLP.
- Ensure the summarizer maintains the original meaning and key points of the text.
- Create an intuitive user interface for easy interaction with the summarizer.

### Methodology:

<b> Data Collection: </b>
<p align="justify"> Initially, we searched for suitable datasets from various sources and decided to use the CNN/Daily Mail dataset. We can also easily access the CNN Daily Mail dataset using the `datasets` library in Python.
The CNN Daily Mail dataset is used in this project for text summarization tasks. It consists of news articles and their corresponding summaries, making it an ideal dataset for training and evaluating text summarization models.</p>

link: [kaggle](https://www.kaggle.com/datasets/gowrishankarp/newspaper-text-summarization-cnn-dailymail/code)

### Text Preprocessing:

To prepare the data for summarization, we applied several preprocessing steps:
- **Lower Casing**: Converted all text to lowercase.
- **Removing Special Characters, Numbers and Punctuations**
- **Tokenization**: Split text into individual tokens (words).
- **stop words removal**: Removing stop words

These preprocessing steps help in understanding and processing the text more effectively. The detailed preprocessing steps are demonstrated in the `preprocessing.ipynb` file.

### Summarization Techniques

Implemented both extractive and abstractive summarization techniques:
- **Extractive Summarization**: Selects key sentences from the original text.
- **Abstractive Summarization**: Generates new sentences that convey the same meaning as the original text.

### Extractive Summarization:
Extractive summarization involves selecting key sentences from the original text that best represent the main points of the document. Here is a detailed explanation of the extractive summarization model developed in this project:

1. **Preprocessing**:
   - **Text Cleaning**: The text is cleaned by removing newline characters, content within square brackets, extra spaces, and quotation marks.
   - **Tokenization**: The text is tokenized into sentences using the `nltk.sent_tokenize` function.
   - **Lemmatization and Stop Words Removal**: Using the `spacy` library, each sentence is processed to extract lemmatized words, excluding stop words and non-alphabetic tokens.

2. **Sentence Scoring**:
   - **TF-IDF (Term Frequency-Inverse Document Frequency)**: This technique is used to calculate the importance of words in each sentence. The `TfidfVectorizer` from `sklearn` is utilized to convert the preprocessed sentences into a TF-IDF matrix. Each row in the matrix represents a sentence, and each column represents a unique term in the corpus.
   - **Sentence Sum Scores**: The sum of TF-IDF scores for each sentence is calculated. This sum score represents the importance of the sentence within the document.
   - **Working Of **TF-IDF**:
 # TF-IDF (Term Frequency-Inverse Document Frequency)

## Overview
TF-IDF is a statistical measure used to evaluate the importance of a word in a document relative to a collection of documents. It helps in identifying words that are unique and important to a document compared to others in the collection.

## Working of TF-IDF
TF-IDF is calculated in two main steps:

### Term Frequency (TF)
Measures how frequently a term (word) appears in a document. It is calculated as:

\[ \text{TF}(t, d) = \frac{\text{Frequency of term } t \text{ in document } d}{\text{Total number of terms in } d} \]

Where \( t \) is the term and \( d \) is the document.

### Inverse Document Frequency (IDF)
Measures how important a term is across all documents in the collection. It is calculated as:

\[ \text{IDF}(t) = \log\left(\frac{\text{Total number of documents}}{\text{Number of documents containing term } t}\right) \]

IDF gives higher weight to terms that are rare across documents but occur frequently within a specific document.

### TF-IDF Calculation
Finally, TF-IDF for a term \( t \) in a document \( d \) is given by:

\[ \text{TF-IDF}(t, d) = \text{TF}(t, d) \times \text{IDF}(t) \]

This product determines the relevance of the term to the document.

## Example Calculation
Consider the sentence:





3. **Sentence Selection**:
   - **Ranking Sentences**: Sentences are ranked based on their sum scores in descending order.
   - **Top-N Sentences**: The top-N highest-scoring sentences are selected to form the summary. In this implementation, N is set to 4, meaning the top 4 sentences are selected.

4. **Summary Generation**:
   - The selected sentences are concatenated to form the final summary. The order of the sentences in the summary is preserved based on their original position in the text.

5. **Implementation**:
   - Implementation is in the file `Extractive_Text_Summarization.ipynb`

6. **Results**:
   - The extractive summarization model successfully identifies and selects key sentences that represent the main points of the text.
   -The resulting summary is concise and retains the essential information from the original document.
**Note: No specific dataset was used for developing the extractive summarization model. The model processes and summarizes the given text directly.**


# Updating the REPORt......


