# Web Crawler and Text Classification System

## Overview

This project implements a multithreaded web crawler combined with a deep learning text classification pipeline. It is designed to systematically crawl a specified website, download and save HTML pages, preprocess text data, and train a neural network classifier to categorize textual content into predefined categories. Additionally, it includes a file system watcher to automate processing upon new file creation or modification, and a priority queue to efficiently manage URLs to crawl.

The system leverages  Python libraries such as BeautifulSoup for HTML parsing, Keras/TensorFlow for deep learning, NLTK for natural language processing, and Watchdog for filesystem event monitoring.

## Key Features

### 1. Web Crawler

- **Multithreaded crawling:** Utilizes Python threading to run multiple crawler workers concurrently for efficient crawling.
- **Politeness and revisit control:** Avoids revisiting URLs within 24 hours to reduce server load.
- **URL normalization:** Handles relative URLs and normalizes links to avoid duplicates.
- **Error handling:** Captures and logs URL errors during crawling.
- **Configurable base URL and threads:** Easy customization of the starting point and concurrency level.
- **HTML content saving:** Stores downloaded pages in a structured directory for offline access and processing.

### 2. Text Classification

- **Dataset preparation:** Uses the BBC text classification dataset as an example, with an 80/20 train-test split.
- **Text tokenization:** Converts raw text to numerical features using Keras tokenizer limited to the top 1000 words.
- **Label encoding:** Transforms categorical labels into one-hot vectors for classification.
- **Neural network model:** Implements a simple dense feedforward neural network with dropout for regularization.
- **Training with validation:** Trains the model with early stopping to prevent overfitting.
- **Evaluation:** Reports test accuracy and loss.
- **Confusion matrix visualization:** Displays normalized confusion matrix for model performance insight.
- **Sample predictions:** Prints examples comparing predicted vs actual categories.

### 3. Folder Watcher (Watchdog)

- **Real-time monitoring:** Watches a target directory for new or modified files.
- **Automatic preprocessing:** Triggers text preprocessing and classification upon detecting file changes.
- **Event handling:** Differentiates between file creation and modification events.

### 4. Priority Queue for URL Management

- **Custom priority queue:** Ensures URLs are processed in order of priority with FIFO for same priority items.
- **Prioritization based on content type:** Supports assigning crawling priority based on predefined categories.

### 5. Text Preprocessing Utilities

- **Tokenization and cleaning:** Removes punctuation, stopwords, and short tokens from text documents.
- **Directory processing:** Cleans all documents in a directory, supporting separate train/test splits.
- **Dataset saving:** Provides functionality to save processed datasets for downstream use.

---

## Usage

1. **Crawler Configuration**

   Modify the `conf` dictionary to set the base URL and number of crawling threads.

2. **Prepare Directory**

   The crawler automatically cleans and creates the output directory for storing crawled pages.

3. **Run Crawler Threads**

   Initialize and start multiple instances of the `Crawler` thread to begin crawling and saving web pages.

4. **Train Classifier**

   Use the prepared dataset (`bbc-text.csv`) to train the neural network classifier. Modify hyperparameters as needed.

5. **Monitor Folder**

   Use the `Watcher` class to monitor new or updated files and trigger processing.

6. **Analyze Results**

   Visualize confusion matrices and inspect sample predictions to evaluate classification performance.

---

## Requirements

- Python 3.7+
- Libraries:
  - `numpy`
  - `pandas`
  - `keras` / `tensorflow`
  - `nltk`
  - `beautifulsoup4`
  - `watchdog`
  - `matplotlib`
  - `scikit-learn`
- Download NLTK stopwords before running (`nltk.download('stopwords')`)

---

## Notes

- The classifier example uses a relatively small dataset and simple model for demonstration. For production, consider more advanced architectures and larger datasets.
- The crawler currently saves all crawled HTML files in one directory; this can be extended with more sophisticated file management or database storage.
- The folder watcher enables real-time data processing pipelines for continuous integration of new content.
- URL prioritization helps focus crawler resources on higher-value pages first.

---

## Author
Ahmed El Jouma
Hasan Kalyoncu University
Email: ael.jouma@std.hku.edu.tr
---


