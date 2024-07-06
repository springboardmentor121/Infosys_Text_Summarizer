# INFOSYS SPRINGBOARD INTERNSHIP 2024 
## A Report On Text Summarizer Model
### Initial Design for the Project Work:

![Initial Design Image](</DesignFiles/design image.png>)

# Text Summarizer
## Abstract:
<p align="justify"> This project, developed as the part of Infosys Springboard internship, focuses on creating a Text Summarizer using Natural Language Processing(NLP) techniques. The summarizer aims to reduce the length of documents while preserving key information and meaning, making it easier for users to quickly understand the content of large texts.</p>

## Objectives:
- Develop an automatic text summarization tool [Both Extractive and Abstractive] using NLP.
- Ensure the summarizer maintains the original meaning and key points of the text.
- Create an intuitive user interface for easy interaction with the summarizer.

## Methodology:

<b> Data Collection: </b>
<p align="justify"> Initially, we searched for suitable datasets from various sources and decided to use the CNN/Daily Mail dataset for the preprocessing learning part. Due to its large size, we then chose the Samsum dataset for the abstractive summarization tasks.

- **CNN/Daily Mail Dataset**: This dataset consists of news articles and their corresponding summaries, making it ideal for training and evaluating text summarization models.
  - [Kaggle](https://www.kaggle.com/datasets/gowrishankarp/newspaper-text-summarization-cnn-dailymail/code)

- **Samsum Dataset**: This dataset is specifically used for abstractive summarization.
  - [Samsum](https://hf.co/datasets/samsum)

## Text Preprocessing:

To prepare the data for summarization, we applied several preprocessing steps:
- **Lower Casing**: Converted all text to lowercase.
- **Removing Special Characters, Numbers and Punctuations**
- **Tokenization**: Split text into individual tokens (words).
- **stop words removal**: Removing stop words

These preprocessing steps help in understanding and processing the text more effectively. The detailed preprocessing steps are demonstrated in the `preprocessing.ipynb` file.

## Summarization Techniques

Implemented both extractive and abstractive summarization techniques:
- **Extractive Summarization**: Selects key sentences from the original text.
- **Abstractive Summarization**: Generates new sentences that convey the same meaning as the original text.




# Extractive Summarization:
Extractive summarization involves selecting key sentences from the original text that best represent the main points of the document. Here is a detailed explanation of the extractive summarization model developed in this project:

## 1. **Preprocessing**:
   - **Text Cleaning**: The text is cleaned by removing newline characters, content within square brackets, extra spaces, and quotation marks.
   - **Tokenization**: The text is tokenized into sentences using the `nltk.sent_tokenize` function.
   - **Lemmatization and Stop Words Removal**: Using the `spacy` library, each sentence is processed to extract lemmatized words, excluding stop words and non-alphabetic tokens.

## 2. **Sentence Scoring**:
   - **TF-IDF (Term Frequency-Inverse Document Frequency)**: This technique is used to calculate the importance of words in each sentence. The `TfidfVectorizer` from `sklearn` is            utilized to convert the preprocessed sentences into a TF-IDF matrix. Each row in the matrix represents a sentence, and each column represents a unique term in the corpus.
   - **Sentence Sum Scores**: The sum of TF-IDF scores for each sentence is calculated. This sum score represents the importance of the sentence within the document.
   
   ## TF-IDF (Term Frequency-Inverse Document Frequency)

   ## Overview
   TF-IDF is a statistical measure used to evaluate the importance of a word in a document relative to a collection of documents. It helps in identifying words that are unique and         important to a document compared to others in the collection.
   
   ## Working of TF-IDF
   TF-IDF is calculated in two main steps:
   
   ## 1. Term Frequency (TF)
   Measures how frequently a term (word) appears in a document. It is calculated as:
   
   <i><b> `TF(t, d) = Frequency of term t in document d / Total number of terms in d` </b></i>
   
   Where t is the term and d is the document.
   
   ## 2. Inverse Document Frequency (IDF)
   Measures how important a term is across all documents in the collection. It is calculated as:
   
   <i><b> `IDF(t) = log(Total number of documents / Number of documents containing term t)` </b></i>
   
   IDF gives higher weight to terms that are rare across documents but occur frequently within a specific document.
   
   ## TF-IDF Calculation
   Finally, TF-IDF for a term t in a document d is given by:
   
   <i><b> `TF-IDF(t, d) = TF(t, d) × IDF(t)` </b></i>
   
   This product determines the relevance of the term to the document.
   
   ## Example Calculation
   
   "Siva is a skilled programmer who enjoys solving complex problems."
   
   ### Applying TF-IDF
   
   | Term       | TF           | IDF (Assuming total documents = 1, term occurs in 1 document) | TF-IDF       |
   |------------|--------------|-------------------------------------------------------------|--------------|
   | Siva       | 1/9 = 0.1111 | log(1/1) = 0                                                 | 0            |
   | is         | 1/9 = 0.1111 | log(1/1) = 0                                                 | 0            |
   | a          | 1/9 = 0.1111 | log(1/1) = 0                                                 | 0            |
   | skilled    | 1/9 = 0.1111 | log(1/1) = 0                                                 | 0            |
   | programmer | 1/9 = 0.1111 | log(1/1) = 0                                                 | 0            |
   | who        | 1/9 = 0.1111 | log(1/1) = 0                                                 | 0            |
   | enjoys     | 1/9 = 0.1111 | log(1/1) = 0                                                 | 0            |
   | solving    | 1/9 = 0.1111 | log(1/1) = 0                                                 | 0            |
   | complex    | 1/9 = 0.1111 | log(1/1) = 0                                                 | 0            |
   | problems   | 1/9 = 0.1111 | log(1/1) = 0                                                 | 0            |

## 3. **Sentence Selection**:
   - **Ranking Sentences**: Sentences are ranked based on their sum scores in descending order.
   - **Top-N Sentences**: The top-N highest-scoring sentences are selected to form the summary. In this implementation, N is set to 4, meaning the top 4 sentences are selected.

## 4. **Summary Generation**:
   - The selected sentences are concatenated to form the final summary. The order of the sentences in the summary is preserved based on their original position in the text.

## 5. **Implementation**:
   - Implementation is in the file `Extractive_Text_Summarization.ipynb`

## 6. **Results**:
   - The extractive summarization model successfully identifies and selects key sentences that represent the main points of the text.
   -The resulting summary is concise and retains the essential information from the original document.
   # ROUGE Scores

| Metric     | Recall | Precision | F1-Score |
|------------|--------|-----------|----------|
| **ROUGE-1** | 0.5614 | 0.5333    | 0.5470   |
| **ROUGE-2** | 0.3894 | 0.3697    | 0.3793   |
| **ROUGE-L** | 0.4211 | 0.4000    | 0.4103   |


**Note: No specific dataset was used for developing the extractive summarization model. The model processes and summarizes the given text directly.**


## User Interface

The application features a clean and user-friendly interface built using Streamlit. Below are screenshots of the interface:

### Main Interface

![Main Interface](</InterfaceFiles/interface 1.png>)

### Summary Output

![Main Interface](</InterfaceFiles/interface 2.png>)


# Abstractive Summarization
This project aims to build an abstractive summarization model using the T5 architecture and the Samsum dataset. The model's objective is to summarize dialogues into concise and coherent summaries.

## **1. Initial Setup:**
We start by importing necessary libraries from the Hugging Face `transformers` library and load the Samsum dataset.

## **2. Load and Inspect Dataset:**
The Samsum dataset is loaded, consisting of three splits: train, test, and validation. Each split contains dialogue and summary pairs used for training and evaluation purposes.

| Split          | Features                | Num Rows |
|----------------|-------------------------|----------|
| **Train**      | ['dialogue', 'summary'] | 14732    |
| **Test**       | ['dialogue', 'summary'] | 819      |
| **Validation** | ['dialogue', 'summary'] | 818      |

## **3. Tokenizer Initialization:**

A tokenizer, specifically the T5Tokenizer from the pre-trained t5-small model, is initialized to handle tokenization for both inputs (dialogues) and outputs (summaries).
### T5 Tokinizer:
- The T5 (Text-To-Text Transfer Transformer) tokenizer is designed to handle various text-to-text tasks, where both the input and output are in the form of textual sequences. It's part of the T5 model architecture, which was introduced by Google AI's team.

## **4. pre-processing:**

### Preprocessing Function Steps

1. **Input Preparation**:
   - Combine each dialogue with a prefix "summarize: ".
   - Example: `"summarize: " + dialogue`

2. **Tokenization of Inputs**:
   - Use the tokenizer to convert the prepared input texts into tokenized representations suitable for model input.
   - Parameters:
     - `max_length=512`: Limit the maximum length of input sequences to 512 tokens.
     - `truncation=True`: Truncate sequences longer than `max_length`.
     - `padding="max_length"`: Pad sequences shorter than `max_length` to ensure uniform input size.

3. **Tokenization of Summaries**:
   - Tokenize the summary texts to prepare them as model targets (labels).
   - Use the tokenizer's target tokenizer context (`tokenizer.as_target_tokenizer()`) for proper label tokenization.
   - Parameters:
     - `max_length=150`: Limit the maximum length of summary sequences to 150 tokens.
     - `truncation=True`: Truncate summaries longer than `max_length`.
     - `padding="max_length"`: Pad summaries shorter than `max_length`.

4. **Formatting Model Inputs**:
   - Store the tokenized inputs and labels in a dictionary (`model_inputs`).
   - Assign the token IDs of the labeled summaries to `"labels"` in the `model_inputs` dictionary.

5. **Return**:
   - Return `model_inputs`, which now contains tokenized inputs and corresponding labels suitable for training the model.


