# Project Log
## Nov 30, 2017
#### Redesign Categorization Workflow

- Update the Categorization.csv file by adding tier, themes, and keywords
    - I removed the *execution behavior* as I think the Verb Phrase detection can 
    do better than defining verbs manually -- remain to be examined
    - We can always add *execution behavior* back if we want a pre-defined 
    behavior for reporting-purposes, and at that time, we will need to cluster 
    similar verbs together
        - For example: how many feedbacks are about "adding a feedback"
- Create a class for categorization dictionary and a function dedicated to 
read and store the dictionary
- Noun Phrases can  be a supplement to Verb Phrases in keyword detection. When 
no keyword is identified in Verb Phrases, use keywords from Noun Phrases
    - If no keywords are identified in NP and VP, search for keywords in the
    entire text
    - Idea: we may improve this by assigning different weights to keywords from
    None Phrases and from Verb Phrases
- Extract the key phrases for actions: Use the identified keyword as a clue to 
extract the original phrases in the sentence
    - If the keyword is in Verb Phrase, identify that Verb Phrase and use that
    as the action phrase
    - Otherwise, identify the location of the keyword in the original feedback
    text, tract back by up to 2 words, and use that phrase for the action phrase.
    
<br>

## Jan 7
Identify problem related to the dataframe length in data processing
- When iterating through the dataframe in categorization part, the index will go beyond the length of the dataset.
- Solution: save the dataframe into a csv file into a local path and reload it, the problem will get solved without 
the need of any other changes
- Try to cut the dataframe length by `df = df[:len(df)]`, cannot solve the problem

Add a summarize function to summarize the issue
- Now just an easy trick: use the first action identified or if there is no action identified, simply give the sentiment
as "General Positive Feedback", etc.

<br>

## Jan 18
Reformat the outputs to remove the quotation marks around the outputs in components, actions, etc.

<br>

## Jan 22
[x] Revise the output format of Categorization
[x] Clustering
[x] Issue summarization for same cluster of feedbacks

<br>

## Feb 12
[x] Extract keywords for each clusters
- Select keywords from VP, NP, and Actions
- Skip stop words and keywords
- Recover from stemmed words

<br>

## Feb 18
[x] Generate synonyms and keywords for Components: 
- Goal: the user only need to give in a list of Components, and the system can automatically generate the relevant keywords
- Approach: 
    - Use WorkNet to find synonyms: accurate but does not help in finding non-synonyms but relevant words
        - Example: find `spotlight` for `highlight`, `TV` for `video`, `universal resource locator` for `URL`
        - Filter out the synonyms whose similiarity score is below 0.9
    - Find all the high frequent words from the original translated feedbacks, and match them with the component based on semantic similarity
        - Does not help, thus abandoned 
    - Cut terminality: cut `History/cookies/cache` into `history`, `cookies`, and `cache` and find synonyms individually
    
<br>

## Questions
- Shall we set up categories for: 
    - Menu
    
## To-Do
- Build up a feedback database
- Develop a function to extract high frequent verb and noun associate with a given
component
    - Input: a keyword (component)
    - Output: 
        - A list of top frequent verb with corresponding percentage
        - A list of top frequent noun with corresponding percentage
- Pull out the top 100 frequent keywords in the feedback database
- Build up a parameterized classifier
- Cannot extract the Verb Phrase `sort my favorites`
    - `my` is `PRP$`
    - `sort the favorites` is extractable
    - For now, we can still extract the keyword `favorites` and use that as a 
    clue

<br>


    