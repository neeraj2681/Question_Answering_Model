# Question_Answering_Model
A BERT based question answering model for Wikipedia Pages 

The model utilises BERT to find the span of an answer for a given question and context.

#How the documents are retrieved
Based on the question given by the user, the model first tries to fetch top 10 documents from the Wikipedia using Wiki library in Python. Among the 10 documents only first 2 are used to find the answer.

#Chunking the Wikipedia articles
Because the model can't have input length(question + context) greater than 512 tokens, the Wikipedia documents retrieved are broken into chunks of maximum 512 length and then sequentially fed to the model.

#length of each chunk
Now, each document will have n answers where n is the number of chunks(roughly equals ceil(l/(512 - q)), where l = length of Wikipedia article, q = length of th question) for that particular document. 

#One particular best answer from all the chunks
Hence, to get the best answer from all the chunks, sum of maximum from answer_start_scores and maximum from answer_end_scores is calculated for each chunk and then the answer returned by the chunk with the maximum sum is considered to be most plausible.

#What is answer_start_score and answer_end_scores
Here, for an answer span, answer_start_scores and answer_end_scores contains the log likelihood of each word being the starting word and ending word respectively.
