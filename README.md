# NLP_text-summarisation
text summarisation of the document whose frequency is more than 1.5 times the avarage


Extractive
step1 :
====================================================================================================================
score each and every word (except stop word,))
stemming

explanation : here we will extract all the words preseent in the document and we will take out the frequency of the each word.
before taking the frequency we will do stemming operation.and we can do mwe tokeniser to get the words with required combination

********************************************************************************************************************
code :
tokenizer = MWETokenizer([('J.', 'P.', 'Morgan', '&', 'Co.')])
words = tokenizer.tokenize(WhitespaceTokenizer().tokenize(all_text))

********************************************************************************************************************
then we will take frequency of the each word as score for the word
====================================================================================================================
step 2
*******************************************************************************************************************
score each sentence -- death is a reality death = 5 reality = 6 Total = 11

explanation :
here we will take each sentence. and we will score the sentence. this can be done by adding all the the score of the words present in  the perticular sentence except the stop words
********************************************************************************************************************
code :
********************************************************************************************************************
def score_sen(text):
    sentences = sent_tokenize(text)
    score_of_sentences = []
    for sentence in sentences:
        words = [word for word in WhitespaceTokenizer().tokenize(sentence)]
        count = 0
        freq = Counter(words)
        for word in words:
            if word in freq.keys():
                count = count+freq[word]
        score_of_sentences.append(count)
    print(len(score_of_sentences))
    return(score_of_sentences)
   
===================================================================================================================

step3 :
*******************************************************************************************************************
normalising the sentence : normalise the sentence score =  Total score of sentence/total number of words in a sentence
def text_summary(text):
    score = score_sen(text)
    sentences = sent_tokenize(text)
    summary_text = []
    for i in range(len(score)):
        if score[i] > np.ceil(2*np.mean(score)):
            summary_text.append(sentences[i])
    print(len(summary_text))
    return('. '.join(summary_text))
*********************************************************************************************************************
avarage of the number

here in the above code we are fetching all the sentence which are having the score greater than the average * 2. 
display all the sentence whose score is greater than average * 2
