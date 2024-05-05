---
layout: wide_default
---  

## Summary Section

The purpose of this assignment was to conduct sentiment analysis on the S&P500 companies. This was done by pulling data from downloaded 10K filings off of SEC Edgar. Once this was done, the data was cleaned. Afterwards, I imported the given dictionaries (LM and ML) and also created my own small one for 3 other topics. this made for 5 different variables each having their own positive and negative versions. The additional topics were regulatory compliance, social impact, and innovation/technology. After this was done, I looped this code to run through all download firm 10Ks. From there I conducted analysis based on the correlation between the sentiment of a firm and its returns.

## Data Section

What is the sample?

    The sample is data provided from the 10K filings from SEC Edgar. This includings the filing dates, ticker symbols, accession numbers, and returns.

How are the return variables built and modified?

    The return variables are stored in a dataframe as decimal values (can be both positive and negative). 

How are the sentiment variables are built and modified?

    The provided sentiment variables are read from their appropriate file paths from the inputs folder. They are then compared to the words in the 10K documents to see if any match, and if so, how many of those do out of all of the words in the document. This gives us a percentage of positive and negative sentiment per variable.
    
    The additional sentiment variables are originally stored in a list full of strings that eventually get transformed into the (word|word|word...etc) format that NEAR regex prefers using a join function. Then the number of those words found in each 10K document is compared to the number of words in total to see what percentage of words actually relates to these topics

A description of how you set up the near_regex function (partial = true or false, distance = what) and why you chose the values you did.

    I set up the near_regex function with partial being true. This is because I wanted the flexibility of being able to search for a relative fit of the pattern desired. A completely exact fit felt unrealistic for me as wording is not always phrased the way you think it will be. For the distance, I left it default because I believe the default value of within five words highlights how well each company actually dedicates (or does not dedicate) their efforts towards that topic of sentiment analysis. A broader range would have allowed for more leway to get mixed messages involved when the words fit but are not discussing the topic at hand.

Why did you choose the three topics you did for the “contextual sentiment” measures?

    I chose regulatory compliance, social impact, and innovation/technology as the three topics for my contextual sentiment because i believe those are pretty well measured in a 10K filing based on the wordage that is used. Additionally, it gives us a hollistic view into the company, more than just its financials, allowing us to make better investment decisions.

Show and discuss summary stats of your final analysis sample

Do your “contextual sentiment” measures pass some basic smell tests?

    I believe my contextual sentiment measures pass some basic smell tests because they returned values that I was sort of expecting to see. Additionally, the words i specified were actually found in the official 10K documents which makes me decently confident in the sentiment variable lists I created. The sentiment measures also worked with diverse data providing additional confidence that they infact are working as they should.

Smell tests: Is something fishy? (What you look for depends on the setting.)

    Something that I thought was a little strange is that even though we downloaded data for S&P500 firms, I only got 498 firms. I am not exactly sure why the other two firms went missing or where they are. I also got zero for one sentiment analysis variable despite how many decimal places I went to which made me think I was doing something wrong. But it actually ended up working for other documents so I made the conclusiom that I ran into an outlier initially.

Do you have variation in the measures (i.e a variable is not all the same value)?

    Yes, the variables are never all the same values for any firms.

Are industries the industries you expect talking about your subject positively or negatively?

    the industries I expect are talking about the topics I picked in a way that is expected. Industries that you would believe would be associated with lower environmental and social impacts score lower as opposed to ones that rely heavily on customer engagement and outreach. A general trend however, all companies tend to score high on regulatory compliance which is not surprising considering the fact that they are in the S&P500.



#### How many words are in the LM positive dictionary?
```
count=0

csv_file_path = "inputs/LM_MasterDictionary_1993-2021.csv"

# Open the CSV file and read positive words
LM_positive_words = set()
with open(csv_file_path, "r", encoding="utf-8") as csv_file:
    csv_reader = csv.DictReader(csv_file)
    for row in csv_reader:
        if int(row["Positive"]) > 0:
            count+=1
```
Answer: 347

#### How many words are in the LM negative dictionary?
```
count=0

csv_file_path = "inputs/LM_MasterDictionary_1993-2021.csv"

# Open the CSV file and read negative words
LM_negative_words = set()
with open(csv_file_path, "r", encoding="utf-8") as csv_file:
    csv_reader = csv.DictReader(csv_file)
    for row in csv_reader:
        if int(row["Negative"]) > 0:
            count+=1
print(count)
```
Answer: 2345

#### How many words are in the ML positive dictionary?
```
file_path = "inputs/ML_positive_unigram.txt"

# initialize an empty list to store positive words
ml_positive_words = []

if os.path.exists(file_path):
    with open(file_path, "r") as file:
        for line in file:
            ml_positive_words.extend(line.strip().split())
    ml_positive_words = list(set(ml_positive_words))
print(len(ml_positive_words))
```
Answer: 75

##### How many words are in the ML negative dictionary?
```
file_path = "inputs/ML_negative_unigram.txt"

# initialize an empty list to store positive words
ml_negative_words = []

if os.path.exists(file_path):
    with open(file_path, "r") as file:
        for line in file:
            ml_negative_words.extend(line.strip().split())
    ml_negative_words = list(set(ml_negative_words))
print(len(ml_negative_words))
```
Answer: 94

## Results


```python

```
