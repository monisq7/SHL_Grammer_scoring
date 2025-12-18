# SHL_Grammer_scoring
Grammar Scoring Engine from Voice Samples
Project Overview


This project implements an end-to-end Grammar Scoring Engine that predicts a continuous grammar score (0–5) from 45–60 second spoken audio samples.

The system converts speech to text using automatic speech recognition (ASR) and extracts interpretable linguistic and fluency features, which are then used to train a regression model.


The solution is designed to be:


Explainable


Modular


Reproducible


Extensible for research

**Problem Formulation**


Input: Audio file (.wav)


Output: Grammar score (continuous)


Task Type: Regression


Evaluation Metrics:


Root Mean Squared Error (RMSE)


Pearson Correlation Coefficient

**Accuracy is not applicable, as this is not a classification problem.
**


**System Architecture
**


Audio (.wav)


   ↓

   
Whisper ASR (Speech → Text)
   
   
   ↓

   
Linguistic & Fluency Feature Extraction
   
   
   ↓

   
Regression Model
   
   
   ↓

   
Grammar Score Prediction



**Dataset Structure
**


dataset/


├── train.csv


├── test.csv


├── sample_submission.csv


├── audios_train/


│   └── *.wav


└── audios_test/
    └── *.wav


train.csv → filename, label

test.csv → filename

label is a continuous grammar score in range 0–5

**Feature Engineering 
**


1️ Lexical Features
Feature	Description
total_words	Total number of words
avg_word_len	Average word length
type_token_ratio	Vocabulary richness


2️ Syntactic (Grammar) Features
Feature	Description
num_nouns	Number of nouns
num_verbs	Number of verbs
num_adjs	Number of adjectives


3️ Sentence Structure Features
Feature	Description
total_sentences	Sentence count
avg_sentence_len	Average words per sentence


4 Fluency Features (ASR-based)
Feature	Description
num_segments	Whisper speech segments
avg_segment_duration	Average pause/flow duration


5️ Disfluency Features
Feature	Description
filler_count	Count of filler words (uh, um, like, etc.)
 Model

Algorithm: Gradient Boosting Regressor

Why?

Handles non-linear feature interactions

Robust on small-to-medium datasets

Interpretable feature importance

Evaluation Strategy

Train–Validation Split: 80/20



Metrics:

RMSE

Pearson Correlation


Cross-validation: 5-fold RMSE (optional)


Example Evaluation Code
rmse = np.sqrt(mean_squared_error(y_val, val_preds))
pearson_corr, _ = pearsonr(y_val, val_preds)

Inference & Submission

The test set is never used for evaluation

Final predictions are generated only after model finalization


Output file format:

filename,label
audio_001.wav,3.42
audio_002.wav,4.11

** How to Run
**


Install dependencies:

pip install openai-whisper nltk scikit-learn tqdm scipy


Download dataset and place in:


/kaggle/input/shl-dataset/



Run the notebook end-to-end

Upload submission.csv to Kaggle

**Limitations
**


ASR transcription errors can affect grammar scoring

Acoustic features (pitch, energy) are not included

Dataset size is relatively small


**Future Improvements
**


Add acoustic features (MFCCs, pause duration)

Use pretrained language models (BERT, RoBERTa)

Hybrid audio + text scoring model

Error-level grammar detection

Feature ablation studies


**Author
**


Mohammad Monis Khan
Research Assistant | NLP & Speech Processing
📍 India

🏁 Conclusion

This project demonstrates a research-grade, explainable approach to grammar scoring from spoken language. The modular design allows easy experimentation and extension, making it suitable for both industrial evaluation and academic research.
