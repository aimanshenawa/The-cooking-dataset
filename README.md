# The-cooking-dataset

## Description
The purpose of this dataset is to evaluate Large Language Models (LLMs) in a cooking scenario. It contains different phases of cooking (Preperation, Cooking, Serving, Eating and Cleaning). Further it is divided into five different question types, depicting different scenarios one can face whilst cooking. The question types are the following:
- Immediate prediction - dictionary type
- Yes/No questions
- Multiple choice questions (MCQ)
- Likelihood questions
- Evaluation of conversation

Total count is as follows:

| Question type                    | No. of questions |
|----------------------------------|------------------|
| Immediate prediction - dictionary| 51               |
| Immediate prediction - yes/no    | 50               |
| MCQ                              | 51               |
| Likelihood prediction            | 59               |
| Evaluation of conversation       | 50               |
| **Total**                        | **261**          |


## Dataset Details
The dataset is in csv format.

The dataset contains the following columns:

1. **phase_id**: Describes which phase of the cooking the question relates to; Phases are: Preperation, Cooking, Serving, Eating and Cleaning
2. **question_type**: Type of the question being evaluated, there are five question types (see table above for detailed count), they are labeled: dictionary\_return, yes\_no\_return, likelihood\_return, mcq, evaluation\_of\_conversation 
3. **number\_of\_questions**: The number of questions related to the current question. Possible values are 1 and 2, out of which only evaluation\_of\_conversation have 2 questions.
4. **question1**: The first question (out of 2). If number\_of\_questions = 1, then this is the only question for the LLM to answer.
5. **question2**: The second question (out of 2). Can be N/A, if number\_of\_questions = 2. If number\_of\_questions = 2, then this is the second prompt for the LLM.
6. **answer\_choices**: Specifies if there is a specific return type. 
7. **expected\_return\_type**: Specifies if there is a particular type of return, dictionary or string.
8. **expected\_answers\_question1**: The ground truth; what is labeled as a correct answer for question 1.
9. **expected\_answers\_question2**: The ground truth; what is labeled as a correct answer for question 2.
10. **comments**: Comments from the creator


### Immediate prediction - dictionary
For this question type, the collumn **question1** contains a prompt, describing a specific object. It is the LLM's taks to understand which object is referred to, and then predict the most likely room, locationa and identify other unique traits the object could have, to be returned in a dictionary format.

E.g.: A prompt could be: **Can you get me the utensil for stirring?**, for which the expected answer is {'object': 'spatula', 'cleanliness': 'clean', 'room' : 'kitchen', 'location': 'drawer'} , among others. If there are multiple acceptable answers, then they are seperated by newlines. All answers are found in expected\_answers\_question1.

### Immediate prediction - yes/no
For this question type, the collumn **question1** contains a question, for which the expected answer is either "yes" or "no".

E.g. **My kid wants to help out, is it fine for her to wash all the vegetables?**, for which the expected answer is: **yes** (can be accessed in expected\_answers\_question1)

### MCQ
In this question type, **question1** contains an initial description, followed by four alternatives, all seperated by newlines. For the alternatives, there are three distractors and one option which is considered the correct answer.

E.g.: 
My recipe calls for half a dozed of eggs do I then prepare
A. 4 eggs
B. 5 eggs
C. 6 eggs
D. 7 eggs

For which, the correct alternative is **C**, retrieved by calling expected\_answers\_question1 for that particular question.

### Likelihood prediction
**question1** contains a question for which the answer is a likelihood, currently the following likelihoods have been considered: very unlikely, unlikely, likely, very likely. However this can be expanded to include neutral as a fifth option in future work.

E.g. **I left the milk out on the counter overnight. What's the likelihood of it being fresh?**

### Evaluation of conversation
In this question type there are two questions. Firstly, **question1** includes a fictional conversation history between a robot (R) and a user (U), followed by a dictionary, which aims to extract all semantic information of a refferred object, and lastly the question: **Was semantic extraction successful?** which has the answer "yes" if all semantic information was successfully extracted to the dictionary, and no - followed by a corrected dictionary, if the extraction was erroneous, incorrect or failed in any other way.

The second question, **question2**, is a question with a yes/no return.

E.g.
question1 = """
U: Hand me the tool for stirring  
R: Might it be a spatula you are talking about? Used for example for mixing food
U: Yes!
R: Is it clean?
U: Yes
{'object': 'spatula', 'location': 'drawer', 'cleanliness':'clean'}
Was semantic extraction successful?
"""

question2 = Given this conversation history, is it correct to assume that the user is about to pour soup for dinner?








