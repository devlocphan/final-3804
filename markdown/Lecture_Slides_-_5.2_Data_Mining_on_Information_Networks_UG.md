## Slide 1

### Lecture 11: Data Mining on Information Networks

3031ICT: Applied Data Mining  
3804ICT: Data Mining

Dr Can Wang (Gold Coast)  
School of Information and Communication Technology

## Slide 2

### Data Mining on Information Networks

- Information Networks
- Social Network Analysis
  - Centrality
  - Prestige
- Sentiment Analysis
  - SA Problems
  - Document sentiment classification
  - Sentence subjectivity & sentiment classification
- Summary

## Slide 3

### Information Networks

- Information networks: consist of a large number of interacting, multi-typed components, such as human social activities, communication and computer systems, as well as biological networks.
- The information network analysis has gained extremely wide attentions from researchers in many disciplines, such as computer science, social science, physics, and so on.
- The basic paradigm is to mine hidden patterns through mining link relations from networked data.

## Slide 4

### Social Network Analysis

- Social network is the study of social entities (people in an organization, called actors), and their interactions and relationships.
- The interactions and relationships can be represented with a network or graph,
  - each vertex (or node) represents an actor and
  - each link represents a relationship.
- From the network, we can study the properties of its structure, and the role, position and prestige of each social actor.
- We can also find various kinds of sub-graphs, e.g., communities formed by groups of actors.

## Slide 5

### Social Network and Web

- Social network analysis is useful for the Web.
  - Each page: a social actor and
  - Each hyperlink: a relationship.
- Many results from social network can be adapted and extended for use in the Web context.
- We study two types of social network analysis, centrality and prestige, which are closely related to hyperlink analysis and search on the Web.

## Slide 6

### Centrality

- Important or prominent actors are those that are linked or involved with other actors extensively.
- A person with extensive contacts (links) or communications with many other people in the organization is considered more important than a person with relatively fewer contacts.
- The links can also be called ties. A central actor is one involved in many ties.

[Figure: A network illustrates actors connected by ties; central actors have more extensive connections.]

## Slide 7

### Degree Centrality

- Undirected Graph: In an undirected graph, the degree centrality of an actor \(i\) (denoted by \(C_D(i)\)) is simply the node degree (the number of edges) of the actor node, denoted by \(d(i)\), normalized with the maximum degree, \(n-1\).

$$
C_D(i)=\frac{d(i)}{n-1}
$$

- The value of this measure ranges between 0 and 1 as \(n-1\) is the maximum value of \(d(i)\).

[Figure: A graph with three vertices and three edges. A second, directed graph has three vertices and four directed edges; a double arrow represents an edge in each direction.]

## Slide 8

### Closeness Centrality

- The basic idea of closeness centrality is that an actor \(i\) is central if it can easily interact with all other actors.
- Let the shortest distance from actor \(i\) to actor \(j\) be \(d(i,j)\) (measured as the number of links in a shortest path).
- Undirected Graph: The closeness centrality \(C_C(i)\) of actor \(i\) is defined as

$$
C_C(i)=\frac{n-1}{\sum_{j=1}^{n}d(i,j)}.
$$

- The value of this measure also ranges between 0 and 1 as \(n-1\) is the minimum value of the denominator, which is the sum of the shortest distances from \(i\) to all other actors. Note that this equation is only meaningful for a connected graph.

## Slide 9

### Prestige

- Prestige is a more refined measure of prominence of an actor than centrality.
- Distinguish: ties sent (out-links) and ties received (in-links).
- A prestigious actor is one who is the object of extensive ties as a recipient.
- To compute the prestige: we use only in-links.
- Difference between centrality and prestige:
  - centrality focuses on out-links;
  - prestige focuses on in-links.
- We study three prestige measures. Rank prestige forms the basis of most Web page link analysis algorithms, including PageRank and HITS.

## Slide 10

### Degree Prestige

- The simplest measure of prestige of an actor \(i\) is its in-degree:

$$
P_D(i)=\frac{d_I(i)}{n-1}.
$$

- Where \(d_I(i)\) is the in-degree of \(i\) (the number of in-links of \(i\)) and \(n\) is the total number of actors in the network.
- In the degree prestige, dividing by \(n-1\) standardizes the prestige value to the range from 0 and 1. The maximum prestige value is 1 when every other actor links to, or chooses actor \(i\).

[Figure: A directed graph with three vertices A, B, C and four directed edges: A → B, C → A, B → C, and C → B. The double arrow between B and C represents an edge in each direction.]

## Slide 11

### Proximity Prestige

- The degree index of prestige of an actor \(i\) only considers the actors that are adjacent to \(i\).
- The proximity prestige generalizes it by considering both the actors directly and indirectly linked to actor \(i\).
  - So we consider every actor \(j\) that can reach \(i\).
- Let \(I_i\) be the set of actors that can reach actor \(i\), called influence domain.
- The proximity is defined as closeness or distance of other actors to \(i\).
- Let \(d(j,i)\) denote the shortest path distance from actor \(j\) to actor \(i\).
- Each link has the unit distance. The average distance:

$$
\frac{\sum_{j\in I_i}d(j,i)}{|I_i|}.
$$

## Slide 12

### Proximity prestige (cont …)

- The proximity prestige is

$$
P_P(i)=
\frac{|I_i|/(n-1)}
{\sum_{j\in I_i}d(j,i)/|I_i|}.
$$

- The numerator is the proportion of actors that can reach actor \(i\).
- The denominator is the average distance.

## Slide 13

### Rank Prestige

- In the previous two prestige measures, an important factor is not considered,
  - the prominence of individual actors who do the “voting”.
- In the real world, a person \(i\) chosen by an important person is more prestigious than chosen by a less important person.
  - For example, if a company CEO votes for a person, this is much more important than a worker votes for the person.
- If one’s circle of influence is full of prestigious actors, then one’s own prestige is also high.
  - Thus one’s prestige is affected by the rank or status of the involved actors.

## Slide 14

### Data Mining on Information Networks

- Information Networks
- Social Network Analysis
  - Centrality
  - Prestige
- Sentiment Analysis
  - SA Problems
  - Document sentiment classification
  - Sentence subjectivity & sentiment classification
- Summary

## Slide 15

### Introduction to Sentiment Analysis

- Sentiment analysis (SA) or opinion mining
  - computational study of opinion, sentiment, appraisal, evaluation, and emotion.
- Why is it important?
  - Opinions are key influencers of our behaviors.
  - Rise of social media → opinion data.
  - Rise of AI and chatbots:
    - Emotion and sentiment are key to human communication.

## Slide 16

### Terms defined - Merriam-Webster

- Sentiment: an attitude, thought, or judgment prompted by feeling.
  - A sentiment is more of a feeling.
  - “I am concerned about the current state of the economy.”
- Opinion: a view, judgment, or appraisal formed in the mind about a particular matter.
  - a concrete view of a person about something.
  - “I think the economy is not doing well.”

## Slide 17

### SA: A fascinating problem!

- Intellectually challenging & many applications
  - A popular research area in NLP, and data mining
    - spread from CS to management and social sciences.
  - A large number of companies in the space globally
    - > 300 in the US alone.
- It touches every aspect of NLP & also is confined.
  - A “simple” semantic analysis problem.
- A major technology from NLP.
  - But it is hard.

## Slide 18

### Two main types of opinions

- Regular opinions: Sentiment/opinion expressions on some target entities
  - Direct opinions:
    - “The touch screen is really cool.”
  - Indirect opinions:
    - “After taking the drug, my pain has gone.”
- Comparative opinions: Comparison of more than one entity
  - E.g., “iPhone is better than Blackberry.”
- We focus on regular opinions and just call them opinions.

## Slide 19

### Definition of Opinion

- ID: abc123 on 29-09-2026 -- “(1) I bought an iPhone 18 Pro yesterday. (2) It is such a nice phone. (3) The touch screen is really cool. (4) The voice quality is great too. It is much better than my Samsung S25. (5) However, my mum was mad with me as I didn’t tell her before I bought the phone. (6) She thought the phone was too expensive”
- Definition: An opinion is a tuple: (target, sentiment, holder, time).
- This definition is concise, but not easy to use.
  - Target can be complex, e.g., “I bought an iPhone. The voice quality is amazing.”
  - Target = voice quality?

## Slide 20

### A more practical definition

- An opinion is a quintuple

  \((\text{entity}, \text{aspect}, \text{sentiment}, \text{holder}, \text{time})\)

  where
  - entity: target entity (or object).
  - Aspect: aspect (or feature) of the entity.
  - Sentiment: +, −, or neu, a rating, or an emotion.
  - holder: opinion holder.
  - time: time when the opinion was expressed.

## Slide 21

### Our example blog in quintuples

- ID: abc123 on 29-09-2026 “I bought an iPhone 18 Pro a few days ago. It is such a nice phone. The touch screen is really cool. The voice quality is great too. It is much better than my old Samsung S25, which was a terrible phone and so difficult to type with its tiny keys. However, my mother was mad with me as I did not tell her before I bought the phone. She also thought the phone was too expensive, …”
- In quintuples
  - (iPhone, GENERAL, +, abc123, 29-09-2026)
  - (iPhone, touch_screen, +, abc123, 29-09-2026)
  - ….

## Slide 22

### Opinion Summary

- With a lot of opinions, a summary is necessary.
  - Not traditional text summary: from long to short.
  - Text summarization: defined operationally based on algorithms that perform the task.
- Opinion summary (OS) can be defined precisely,
  - not dependent on how summary is generated.
- Opinion summary needs to be quantitative.
  - 60% positive is very different from 90% positive.
- Main form of OS: Aspect-based opinion summary.

## Slide 23

### Opinion Summary

A common form of summary is based on aspects: Aspect/feature Based Summary of opinions about iPhone.

**Aspect: Touch screen**

Positive:

- The touch screen was really cool.
- The touch screen was so easy to use and can do amazing things.
- …

Negative:

- The screen is easily scratched.
- I have a lot of difficulty in removing finger marks from the touch screen.
- …

**Aspect: voice quality**

…

[Figure: “Visualization of aspect-based summary of opinions on a cellular phone”. A bar chart for Cellular Phone 1 compares Positive and Negative opinions across GENERAL, Voice, Battery, Camera, Size, and Weight. Exact bar magnitudes are not labeled legibly.]

[Figure: “Visual opinion comparison of two cellular phones”. Grouped bars for Cellular Phone 1 and Cellular Phone 2 compare Positive and Negative opinions across GENERAL, Voice, Battery, Camera, Size, and Weight. Exact bar magnitudes are not labeled legibly.]

## Slide 24

### Subjective vs Objective

- Sentence subjectivity
  - An objective sentence presents some factual information,
  - while a subjective sentence expresses some personal feelings, views, emotions, or beliefs.

## Slide 25

### Subjective Opinions

- Definition: A subjective opinion is a regular or comparative opinion given in a subjective statement.
- For example,
  - “Coke tastes great.”
  - “I think Google’s profit will go up next month.”
  - “This camera is a masterpiece.”
  - “We are seriously concerned about this new policy.”
  - “Coke tastes better than Pepsi.”

## Slide 26

### Objective Sentences with Opinion

- Most opinion sentences are subjective, but objective (or factual) sentences can imply opinions too.
- They express desirable or undesirable facts.
  - “The machine stopped working in the second day”
  - “We bought the mattress yesterday, and a body impression has formed.”
  - “After taking the drug, there is no more pain”
- Such sentences are very hard to handle.

## Slide 27

### Emotion

- Emotion is what SA wants to capture.
- No agreed set of basic emotions of people.
  - Based on Parrott (2001), people have six basic emotions:
    - love, joy, surprise, anger, sadness, and fear.
- Although related, emotions and opinions are not equivalent.
  - Opinion: rational (+/−) view on something.
    - Cannot say “I like”.
  - Emotion: focusing on an inner feeling.
    - Can say “I am angry” or “There is sadness in her eyes”.

## Slide 28

### Definition of Emotion

- Definition (Emotion): It is a quintuple,

  (entity, aspect, emotion_type, feeler, time)

  - E.g., “I am so mad with the hotel manager because he refused to refund my booking fee”
    - Entity: hotel
    - Aspect: manager
    - emotion_type: anger
    - feeler: I
    - time: unknown
  - The definition can also include the cause.

## Slide 29

### Emotion Expressions

1. Use emotion or mood words or phrases.
   - E.g., love, disgust, angry, and upset.
2. Describe emotion-related behaviors.
   - “He cried after he saw his mother” and
   - “After he received the news, he jumped up and down for a few minutes like a small boy.”
3. Use intensifiers: Common English intensifiers include
   - very, so, extremely, dreadfully, really, awfully, etc.

## Slide 30

### Emotion Expressions (conted.)

4. Use superlatives.
   - Many superlative expressions also express emotions, for example, “This car is simply the best”.
5. Use swearing, cursing, insulting, blaming, accusing, and threatening expressions.

## Slide 31

### Assumption and Goal

- Assumption: The doc is written by a single person and express opinion/sentiment on a single entity.
- Reviews usually satisfy the assumption.
  - Almost all research papers use reviews.
  - Positive: 4 or 5 stars, negative: 1 or 2 stars.
- Forum postings and blogs do not follow the assumption.
  - They may mention and compare multiple entities.
  - Many such postings express no sentiments.

## Slide 32

### Sentiment Classification

- Classify a whole opinion document (e.g., a review) based on the overall sentiment of the opinion holder.
  - Classes: Positive, Negative (possibly Neutral).
- An example review:
  - “I bought an iPhone a few days ago. It is such a nice phone, although a little large. The touch screen is cool. The voice quality is great too. I simply love it!”
  - Classification: positive or negative?
- It is basically a text classification problem.

## Slide 33

### Supervised Learning

- Directly apply supervised learning techniques to classify reviews into positive and negative.
- Three classification techniques can be tried:
  - Naïve Bayes, Maximum Entropy, Support Vector Machines (SVM).
- Features: negation tag, unigram (single words), bigram, POS tag, position.
- SVM did the best based on movie reviews.
- Nowadays, deep Learning models with word embedding is state-of-the-art.

## Slide 34

### Features for Supervised Learning

- The problem has been studied by numerous researchers.
- Key: feature engineering. A large set of features have been tried by researchers. E.g.,
  - Terms frequency and different IR weighting schemes.
  - Part of speech (POS) tags.
    - http://universaldependencies.org/u/pos/all.html#al-u-pos/DET
  - Etc.

[Figure: A word-to-tag diagram labeled WORDS and TAGS. Arrows connect words in “the waiter cleared the plates from the table” to their part-of-speech tags; the connections are represented as a table.]

| WORDS | TAGS |
| --- | --- |
| the | DET |
| waiter | NOUN |
| cleared | VERB |
| the | DET |
| plates | NOUN |
| from | PREP |
| the | DET |
| table | NOUN |

## Slide 35

### Lexicon-based Approach

- Using a set of sentiment terms, called the sentiment lexicon.
  - Positive words: great, beautiful, amazing, …
  - Negative words: bad, terrible awful, unreliable, …
- The value for each sentiment term is assigned from [−5, +5].
  - Consider negation, intensifier (e.g., very), and diminisher (e.g., barely).
- Decide the sentiment of a review by aggregating scores from all sentiment terms.

## Slide 36

### Deep Learning

- Recently, deep neural networks have been used for sentiment classification. E.g.,
  - Socher et al used deep learning to work on the sentence parse tree based on words/phrases compositionality in the framework of distributional semantics.
  - Many papers …
  - Also related
    - extract opinion expressions;
    - identify opinion & target relations.

## Slide 37

### Review Rating Prediction

- Apart from classification of positive or negative sentiments,
  - Research has also been done to predict the rating scores (e.g., 1–5 stars) of reviews.
  - Training and testing are reviews with star ratings.
- Formulation: The problem is formulated as regression since the rating scores are ordinal.

## Slide 38

### Sentence Sentiment Analysis

- Usually consist of two steps.
  - Subjectivity classification (Wiebe et al 1999)
    - To identify subjective sentences.
    - Sentence similarity.
    - Naïve Bayesian classification.
  - Sentiment classification of subjective sentences
    - Into two classes, positive and negative.
- But bear in mind
  - Many objective sentences can imply sentiments.
  - Many subjective sentences do not express positive or negative sentiments/opinions.

## Slide 39

### Data Mining on Information Networks

- Information Networks
- Social Network Analysis
  - Centrality
  - Prestige
- Sentiment Analysis
  - SA Problems
  - Document sentiment classification
  - Sentence subjectivity & sentiment classification
- Summary

## Slide 40

### Have a question?
