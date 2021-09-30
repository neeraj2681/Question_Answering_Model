# Question_Answering_Model
A BERT based question answering model for Wikipedia Pages 

The model utilises BERT to find the span of an answer for given question and context pairs.

<h3>How the documents are retrieved</h3>
Based on the question given by the user, the model first tries to fetch top 10 documents from the Wikipedia using Wiki library in Python. Among the 10 documents only first 2 are used to find the answer.<br>

<h4>A sample question for which documents are retrieved</h4>
<img src = "./codes_snap/retrieval_part.png" alt = "retrieval of documents for a particular question">

<h3>Chunking the Wikipedia articles</h3>
Because the model can't have input length(question + context) greater than 512 tokens, the Wikipedia documents retrieved are broken into chunks of maximum 512 length and then sequentially fed to the model.

<h3>length of each chunk</h3>
Now, each document will have n answers where n is the number of chunks(roughly equals <b>ceil(<i>l</i>/(512 - <i>q</i>))</b>, where <i>l</i> = length of Wikipedia article, <i>q</i> = length of th question) for that particular document. 

<h3>One particular best answer from all the chunks</h3>
Hence, to get the best answer from all the chunks, sum of maximum from <code>answer_start_scores</code> and maximum from <code>answer_end_scores</code> is calculated for each chunk and then the answer returned by the chunk with the maximum sum is considered to be most plausible.

<h3>What is answer_start_score and answer_end_scores</h3>
Here, for an answer span, <code>answer_start_scores</code> and <code>answer_end_scores</code> contains the log likelihood of each word being the starting word and ending word respectively.
