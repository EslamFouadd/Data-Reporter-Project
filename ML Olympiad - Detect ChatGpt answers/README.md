
# Dataset Description
The training and test sets contain prompts, which are questions on various things and of multiple categories, and the replies to those prompts in the form of grammatically correct paragraphs.
The prompts include opinion-based questions, general knowledge questions, scientific facts, and special ones to spice things up. each prompt contains an unannounced ratio of human to ChatGpt generated replies, per example ( 1 ChatGpt generated reply, 5 human generated replies).
The data has been approximately split 75%/25% for training/test.

# Files
train.csv - the training set
test.csv - the test set
sample_submission.csv - a sample submission file in the correct format
Columns
prompt - The question or the prompt
answer - The answer given by the target
AI - 0 If the question was answered by a human being, 1 if It is a ChatGpt-generated answer .
