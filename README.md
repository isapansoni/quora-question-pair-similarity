# Quora Question Pair Similarity 

Quora is a place to gain and share knowledge—about anything. It’s a platform to ask questions and connect with people who contribute unique insights and quality answers. This empowers people to learn from each other and to better understand the world.

Over 100 million people visit Quora every month, so it's no surprise that many people ask similarly worded questions. Multiple questions with the same intent can cause seekers to spend more time finding the best answer to their question, and make writers feel they need to answer multiple versions of the same question. Quora values canonical questions because they provide a better experience to active seekers and writers, and offer more value to both of these groups in the long term.

### Problem Statement

- Identify which questions asked on Quora are duplicates of questions that have already been asked.
- This could be useful to instantly provide answers to questions that have already been answered.
- We are tasked with predicting whether a pair of questions are duplicates or not.

 ### Data Overview 
- Data will be in a file Train.csv 
- Train.csv contains 5 columns : qid1, qid2, question1, question2, is_duplicate 
- Size of Train.csv - 60MB 
- Number of rows in Train.csv = 404,290


have done advance NLP feature extraction to resolve this case study 

### NLP and Fuzzy Features

Definition:

Token: You get a token by splitting sentence a space
Stop_Word : stop words as per NLTK.
Word : A token that is not a stop_word
Features:

**cwc_min** : Ratio of common_word_count to min lenghth of word count of Q1 and Q2 
**cwc_min** = common_word_count / (min(len(q1_words), len(q2_words))

**cwc_max** : Ratio of common_word_count to max lenghth of word count of Q1 and Q2 
**cwc_max** = common_word_count / (max(len(q1_words), len(q2_words))

**csc_min** : Ratio of common_stop_count to min lenghth of stop count of Q1 and Q2 
**csc_min** = common_stop_count / (min(len(q1_stops), len(q2_stops))

**csc_max** : Ratio of common_stop_count to max lenghth of stop count of Q1 and Q2
**csc_max** = common_stop_count / (max(len(q1_stops), len(q2_stops))

**ctc_min** : Ratio of common_token_count to min lenghth of token count of Q1 and Q2
**ctc_min** = common_token_count / (min(len(q1_tokens), len(q2_tokens))

**ctc_max** : Ratio of common_token_count to max lenghth of token count of Q1 and Q2
**ctc_max** = common_token_count / (max(len(q1_tokens), len(q2_tokens))

**last_word_eq** : Check if First word of both questions is equal or not
**last_word_eq** = int(q1_tokens[-1] == q2_tokens[-1])

**first_word_eq** : Check if First word of both questions is equal or not
**first_word_eq** = int(q1_tokens[0] == q2_tokens[0])



**abs_len_diff** : Abs. length difference
**abs_len_diff** = abs(len(q1_tokens) - len(q2_tokens))



mean_len : Average Token Length of both Questions
mean_len = (len(q1_tokens) + len(q2_tokens))/2



fuzz_ratio : https://github.com/seatgeek/fuzzywuzzy#usage http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/



fuzz_partial_ratio : https://github.com/seatgeek/fuzzywuzzy#usage http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/



token_sort_ratio : https://github.com/seatgeek/fuzzywuzzy#usage http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/

token_set_ratio : https://github.com/seatgeek/fuzzywuzzy#usage http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/

longest_substr_ratio : Ratio of length longest common substring to min lenghth of token count of Q1 and Q2
longest_substr_ratio = len(longest common substring) / (min(len(q1_tokens), len(q2_tokens))

## models we used for case study

1) Logistic Regression
2) Linear SVM
3) XGboost

## Extensions 

1) we can use TF-IDF or bag of words vectorization instead of GLOVE word2vec representation
2) We can use Naive Bayes model for this model