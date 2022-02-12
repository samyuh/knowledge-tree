---
title: "Processamento e Recuperação de Informação"
description: "Resumos da cadeira"
aliases: "PRI"
tags: "#uc"
---

# PRI - Information Processing and Retrieval
## **1. Information processing**

## Data, metadata and information
- **Data:** facts known by direct observation, measured on a specific scale.
- **Metadata:** "data about data", provides information about the data (date, author, format, version, permissions, etc.
- **Information:** processed, structured and organised data with a context/meaning, which enables decision making.

## Information Life Cycle
- **Occurrence:** discovery, design or creation.
- **Transmission:** access, retrieval, transmission and networking.
- **Processing and Management:** collection, validation, modification, classification, filtering, sorting and storing.
- **Usage:** monitoring, interpreting, planning, decision-making, learning, etc.

## Data Processing Patterns
### ETL 
- Extract-Transform-Load Framework.
- Extract data from the source system, operate over the data and transform it, publish the data to the target system.
- Usually associated with classic centralised IT driven operations.

### EtLT
- Extract-Load-Transform Framework.
- Introduces a transformation step before the loading, but loads before the full transformation.
- More well-suited for division of responsibilities in multidisciplinary teams.

### OSEMN
- Obtain (gather data), Scrub (clear, arrange and prepare), Explore (visualize and experiment), Model (create a statistical model), Interpret (draw conclusions and evaluate).
- Usually represented in a linear model, but applied iteratively.


## Data Processing Challenges
- Diversity of data sources in various dimensions (ownership, interface, volume, cleanliness, validity, latency, etc.).
- Data quality problems (missing data, inconsistent values, precision problems, duplicate values, etc.).
- Data storage model choice (relational, document or graph).


## Challenges and Techniques
### Data Cleaning:
- Challenges:
    - Identification and fixing of data quality issues;
    - Reduction/Selection of data from the collection;
- Techniques:
    - Outliers removal;
    - Missing values substitution;
    - Sampling of the collection.

### Data Preparation:
- Challenges:
    - Choice of data to use (choosing relevant data subsets and fields);
    - Combination of multiple sources of data (linking the corresponding records);
    - Adapt the results to a size and shape that enables follow-up steps.
- Techniques:
    - Data transformation (transform data to improve analysis or manipulation);
        - Normalisation of values;
        - Scaling values to the same range;
        - Non-linear transformation to deal with skewed distributions;
        - Discretisation or binning (transform continuous values into ordered and categorical ones).
    - Synthesis of data (derive new attributes from existing data);
        - Maximum, minimum, average values;
        - Difference between two numerical attributes;
        - Most important keywords/topics from a textual field.
    - Data integration (combine data from multiple sources).
        - Enrich individual records with data from external sources.

### Data Presentation:
- Challenges:
    - Visualisation of the data;
    - Interpretation of the results obtained. 
- Techniques:
    - Exploratory visualisation of the data (to detect disparities, choose adequate methods, etc.);
    - Plotting of descriptive statistics (to observe the application of methods and track the pipeline execution);
    - Result evaluation (compare results between different pipeline executions).


## Data pipelines
### Importance
A reliable, scalable and maintainable pipeline is key to keep the data processing track (that transforms data from a source to a destination) simpler and more stable throughout different executions. 

### Makefiles
Makefiles can be used to document and setup data pipelines, since they enable the definition of execution rules on specific targets, being useful to automate software build processes (such as data processing).

----------------------

## **2. IR tasks and systems**
## Information Retrieval vs. Data Retrieval
- **Data Retrieval:** Data Retrieval is the action of determining which documents of a certain collection explicitly contain the query keywords. It tries to provide a solution to a database user.
- **Information Retrieval:** Information Retrieval is the attempt of satisfying a certain information need. It solves the problem of retrieving information about a subject or topic. Instead of looking for the presence of keywords, it searches for the presence of information that can answer the query.
- **Key difference:** Failure in DR (retrieving a document that does not contain the keywords) means a total failure. In IR, a failure is defined against the information need. 


## Examples
- **DR systems:** Relational database.
- **IR systems:** Google, Amazon, Bing, etc.


## Retrieval tasks evaluated in TREC
- TREC is organized into tracks, each of them providing a set of documents and queries.
- The participants have to build a system for the queries will be held against.
- They must submit their created system's responses to that set of queries.
- These responses are then evaluated by the organisers.
- The details can vary from track to track and from year to year.


## Modules of an IR system
### Crawling
If the document collection is available in the web, the first stage is for a web crawler to retrieve it.

### Indexing
On this stage, he document collection retrieved is stored in the "central repository" (disk storage) and indexed (usually, an inverted index is created, composed of each word and a list of the documents that contain it).

### Retrieval & Ranking
The retrieval process consists of determining which documents satisfy a user query. This query is parsed, expanded and processed against the index to retrieve a subset of documents, which are then ranked in terms of relevance (to the user, considering their query) and the top results are returned to the user.

----------------------

## **3. IR concepts**
## Concept definition
- **Document:** Unit of data of a retrieval system;
- **Collection:** Set of documents over which a retrieval is performed;
- **Term:** Each part of a document that can be indexed (usually words or phrases);
- **Bag of words:** Description of the number of occurrences of words in a document, with no details about their order or structure;
- **Stemming:** Replacing inflected or derived words with their radical word (stem);
- **Inverted Index:** Table that relates a term to its postings list.
- **Vocabulary:** Set of terms in a collection.
- **Postings list:** List of documents containing a term.
- **Information need:** Topic about which the user searches and wants to know more.
- **Query:** What the user conveys to the system to communicate an information need.
- **Results list:** List of documents returned by a specific retrieval.
- **Relevant result:** Result that satisfies or has valuable information for the user's information need.

----------------------

## **4. Vector model**
## Concept definition
- **Term Frequency (tf<sub>t,d</sub>):** Number of occurrences of term *t* in document *d*.
- **Collection Frequency (cf):** Number of occurrences of a term in a collection.
- **Document Frequency (df<sub>t</sub>):** Number of documents in a collection that contain a term *t*.
- **Inverse Document Frequency (idf<sub>t</sub>):** Measurement of the rarity of a term *t* (higher if *t* is rare).
    - idf<sub>t</sub> = log(N/df<sub>t</sub>),
    - N being the number of documents in a collection.


## Tf-idf weight
### **Formula:** tf-idf<sub>t,d</sub> = tf<sub>t,d</sub> x idf<sub>t</sub>

### **Concept:**
- Assign a weight to term *t* in document *d* for discrimination during the evaluation/ranking of results.
- The weight of term *t* is:
    - higher when *t* has many occurrences in very few documents;
    - lower when *t* has few occurrences in *d* or occurs in many documents;
    - lowest when *t* occurs in virtually all documents.


## Document ranking
- The rank of a document *d* against a query *q* according to the vector model is the sum of the weight of each of the terms of *q* that occur in *d*.
- Score<sub>(q,d)</sub> = $\sum_{t\ in\ q}$ tf-idf<sub>t,d</sub>.

----------------------

## **5. Evaluation**
## Concept definition
- **Precision:** Percentage of documents in a results list that are relevant.
- **Recall:** Percentage of the total relevant documents that were retrieved.
- **Interpolated Precision:** Highest precision found for any recall level higher than a defined bound.
- **Precision at k:** Percentage of results that are relevant on the first k for the query.
- **R-Precision:** Precision at k, for k equal to the number of relevant results for the query.


## Test collection components
- Document collection;
- Test suite of information needs, expressible as queries;
- Set of relevance judgements, standardly a binary assessment of either *relevant* or *nonrelevant* for each query-document pair.


## Relevance judgements
### Definition: 
A relevance judgement is a binary assessment of a document as *relevant* or *nonrelevant* against an information need from the user.

### Ground truth
The relevance judgement decision is referred to as *ground truth*, meaning that it is the basis for the whole evaluation of the retrieval system. Having a set of human-judged query-document pairs (ground truth) is crucial for the evaluation of the accuracy of the system's retrieval methods.


## Average 11-point precision-recall graph
- For each of the 11 recall levels (0, 0.1, 0.2, ...), the 11-point precision-recall graph calculates the mean of the interpolated precision at that recall for each query in the set.


## MAP
### Definition
- Mean average precision consists of a measure that calculates the mean of the Average Precision (average of precision measured every time a relevant result is retrieved) of several information needs.
- For a single information need, the AP approximates the area under the uninterpolated precision-recall curve. The MAP is roughly the average area under the precision-recall curve for a set of queries.

----------------------

## **6. Web search**
## Types of information needs
### Informational needs
- Search for general information on a topic.
- Typically requires gathering information from more than one web page.

### Transactional needs
- Attempt a transaction on the web.
- Can be a purchase, a download, a reservation, etc.

### Navigational needs
- Seek for the website or page of an entity.
- User has the expectation of finding a specific resource. 


## Web search vs enterprise search
- Web search users aren't trained on how to write queries.
- In enterprise search, the users are professionals, and use keywords more wisely, as well as search operators.


## Indexing images
In concept-based image indexing, images are indexed by their anchor text, which usually includes information about their content.


## Ranking signals
Ranking signals fall into different groups:
- Query-independent signals (static) - website date;
- Query-dependent signals (dynamic) - term frequency;
- Document-based signals (content or structural) - being HTML, PDF;
- Collection-based signals - number of in-links;
- User-based signals - number of clicks, browser used, OS used, location or date of the search.


## Bowtie view
### SCC
The SCC (Strongly Connected Component) consists of a group of documents in the collection between which one can navigate and return freely using links.

### IN and OUT
The bowtie view states that a user can pass from any node of IN through SCC to any node of OUT.

### Tendrils and tubes
Tendrils consist of nodes reachable from IN or that can reach OUT. Tubes are the connection of an IN tendril and an OUT tendril, without passing through the SCC.

----------------------

## **7. Link analysis**
## Link-based Signals
### In-links and out-links
In-links are links from other pages to a given pages; out-links are links present in a given page that leads to another page, which represents an endorsement of the latter by the creator of the first.

### Anchor text as a signal
The anchor text (e.g. in links) in a page represents its creator's description of the page to which it leads, which is an important feature for image search and is also incorporated as an additional feature in an inverted index.


## PageRank
The PageRank of a node is a value between 0 and 1, representing the probability of a random surfer to visit said note by choosing, at each step, a random out-link to move to the next page.


## HITS - Hyperlink Induced Topic Search
Query dependent algorithm that, starting with the answer set (e.g. pages containing the keywords), computes two scores for each page:
- **Authority score:** pages with many in-links are called authorities;
- **Hub score:** pages with many out-links are called hubs.

----------------------

## **8. Query processing**
## Main processing techniques
### Document-at-a-time
Calculate complete scores for documents, by processing all term lists, one document at a time. At the end, all documents are sorted according to their score.

### Term-at-a-time
Accumulate scores for documents by processing term lists one at a time. When all terms are processed, the accumulators contain the final scores of all matching documents.


## Optimisation
### Purpose
Query optimisation techniques allow the system to read less data from the index or process fewer documents, which is advantageous when using complex feature functions, to avoid scoring less useful documents, or when using simpler ones, to ignore as much inverted list data as possible.

### Query transformation
Query transformation techniques (e.g. stopwords, stemming, spellchecks, suggestions) can be used to refine the search, in order to reduce the amount of data processed.

### Query expansion
With query expansion techniques (e.g. use of synonyms and related words from a thesaurus, (pseudo) relevance feedback), users give additional input on query words or phrases.

### Relevance feedback
The idea of relevance feedback is to consider user feedback about the initial set of results when improving the final set.

The user marks documents returned by the system as relevant or non-relevant and the system computes a better representation of the information, which is then displayed to the user.

Especially useful for image search, where it may be difficult to express a query in words.

### Pseudo relevance feedback
Users often expect single interactions in search and are reluctant to provide explicit feedback, which is why pseudo relevance feedback automates the manual part, assuming that the top k ranked documents are relevant.

### Implicit relevance feedback
This technique uses indirect sources of evidence (e.g. clicks on links are assumed to indicate that the page was likely relevant for the query), which are less reliable than explicit, but more useful than pseudo relevance feedback.

----------------------

## **9. Entity-oriented search**
## Entity
An entity is an uniquely identifiable thing or object (e.g. people, organisations, products, locations), characterised by its name, type, attributes and relationships to other entities.

### Entity-oriented search
EOS is the search paradigm of organising and accessing information centered around entities, their attributes and relationships.

From a user perspective, entities are natural units for organising information that offer a richer excperience than conventional document-based retrieval systems.

From a machine perspective, entities allow for a better understanding of search queries, document content and users, making search engines more effective.

### Entity description
An entity description, or profile document, is an object created for each entity, containing all the existing knowledge about that entity.

Entity descriptions can be indexed and ranked using existing document retrieval algorithms.

### Entity ranking
With the term-based entity representation, we can use the retrieval models from document ranking for entity scoring by using entities as documents. Most of the effort is put into constructing term-based representations of entities.

Unstructured entity representations with a bag-of-words model usually provide solid performance and a good starting point. Other approaches exist, such as the use of specific characteristics of entities, such as relationships.

### Entity linking
Entity linking is the task of recognising entity mentions in text and linking them to the corresponding entries in a knowledge base.
- Mention detection: identification of text snippets that can potentially be linked to entities;
- Candidate selection: generating a set of candidate entities for each mention;
- Disambiguation: selecting a single entity (or none) for each mention, based on the context.

## Data sources
### Knowledge bases
Knowledge bases organise information around entities, which can be seen as nodes in a graph, with relationships between them as edges.

When it focuses more on the relationships, the term knowledge graph is commonly used.

A standard way of describing entities is the Resource Description Framework (RDF), consisting of a subject (URI of a resource), a predicate (URI of a relationship or property of the subject) and an object (URI of another resource or literal).

### Examples
- Public knowledge bases: DBpedia (extracted from Wikipedia), Wikidata (operated by the Wikimedia Foundation, considers claims - that must be supported by a reference and can contradict each other - instead of facts);
- Proprietary knowledge bases: Google Knowledge Graph, Facebook Entity Graph, Microsoft Satori.

----------------------

## **10. Search user interfaces**
## SUI techniques and elements
### Context
IR evolved to a both system- and user-centered view, with the observation that more specific queries improved the relevance of results, thus a SUI is necessary for users to interact with the system.

Multiple factors concur to the overall user experience:
- Implemented algorithms;
- Existing metadata;
- Design and aesthetics of the UIs.

### Elements
- **Input:** features that allow the searcher to express what they are looking for;
- **Control:** features that help searchers modify, refine, restrict or expand their input;
- **Informational:** features that provide results or information about them;
- **Personalisation:** features that relate specifically to searchers and their previous interactions.

## Evaluation
### IR style
Traditionally, IR systems are evaluated based on datasets, specific tasks, and known best results for each task (calculated by human experts).

Success was limited for this approach, since simple evaluation measures like precision and recall were not sufficient.

### Empirical user studies
Empirical methods are about observing and recording actual user performance (e.g. number of searches, terms per search, results visited, search times, task accuracy). Qualitative methods such as interviews and observations are also possible.

Designing and conducting user studies is hard, because results can be impacted by many factors (e.g. motivation of participants, software bugs) and even small user experience differences (e.g. slight differences in colors).

### Analytical approaches
In analytical approaches, typically low-cost inspection methods are used by evaluators to assess a design.

There are many analytics methods for UI and UX (e.g. heuristic evaluation, cognitive walkthrough) but fewer specifically designed for SUI.

### Choosing an evaluation approach
DECIDE process:
- **D**etermine the goals of the evaluation;
- **E**xplore the specific questions to be answered;
- **C**hoose an evaluation paradigm;
- **I**dentify practical issues in performing such an evaluation;
- **D**ecide how to deal with any ethical issues;
- **E**valuate, interpret and present data.

## Design principles and heuristics
1. Visibility: keep the user informed of what is happening;
2. Language: adopt language that the user can understand;
3. Control and freedom: do not block users in a hole or fixed pathway, instead provide mechanisms for users to recover from them;
4. Consistency: adopt a consistent design;
5. Error prevention: make it hard to do unproductive things (i.e. avoid the need to undo actions);
6. Support recognitions: help users not have to remember what they have done or need to do;
7. Flexibility and efficiency: provide features for experienced users to be more productive and efficient;
8. Aesthetics and minimalism: keep design simple and minimalist;
9. Clear error messages: provide informative and useful error messages;
10. Help and documentation: provide help as documentation, FAQs and examples.

----------------------

# Exercises Manning
## Chapter 6:
### **6.8.)**
The number of documents (*N*) is always finite and the document frequency (*df<sub>t</sub>*) is always a natural number (for any term that exists in the collection), so the result of log(N/df<sub>t</sub>) is always finite.

### **6.9.)**
The idf of a term that occurs in every document is log(1) = 0, so the word is ignored for weighing factors. The same happens with words put in the stopword list.

### **6.10.)**
- tf-idf<sub>car,doc1</sub> = 1.65*27 = 44.55
- tf-idf<sub>car,doc2</sub> = 1.65*4 = 6.6
- tf-idf<sub>car,doc3</sub> = 1.65*24 = 39.6
- tf-idf<sub>auto,doc1</sub> = 2.08*3 = 6.24
- tf-idf<sub>auto,doc2</sub> = 2.08*33 = 68.64
- tf-idf<sub>auto,doc3</sub> = 2.08*0 = 0
- tf-idf<sub>insurance,doc1</sub> = 1.62*0 = 0
- tf-idf<sub>insurance,doc2</sub> = 1.62*33 = 53.46
- tf-idf<sub>insurance,doc3</sub> = 1.62*29 = 46.98
- tf-idf<sub>best,doc1</sub> = 1.5*14 = 21
- tf-idf<sub>best,doc2</sub> = 1.5*0 = 0
- tf-idf<sub>best,doc3</sub> = 1.5*17 = 25.5

### **6.15.)**
Unnormalised:
- doc1 = [44.55, 6.24, 0, 21]
- doc2 = [6.6, 68.64, 53.46, 0]
- doc3 = [39.6, 0, 46.98, 25.5]

Normalised:
- doc1 = [0.897, 0.126, 0, 0.423]
- doc2 = [0.076, 0.787, 0.613, 0]
- doc3 = [0.595, 0, 0.706, 0.383]

### **6.16.)**
They all equal 1, since we are normalising the Euclidean distance, making the length of the vector equal to 1.

### **6.17.)**
**i)** The query vector is q1 = [1, 0, 1, 0].
score<sub>(q1,doc1)</sub> = 0.897 + 0 = 0.897
score<sub>(q1,doc2)</sub> = 0.076 + 0.613 = 0.689
score<sub>(q1,doc3)</sub> = 0.595 + 0.706 = 1.301
The ranking would be doc3 > doc1 > doc2.

**i)** The query vector is q2 = [1.65, 2.08, 1.62, 1.5] / ||q2|| = [0.478, 0.602, 0.469, 0.434].
score<sub>(q2,doc1)</sub> = (0.478*0.897) + (0.6024\*0.126) + (0.434\*0.423) = 0.688
score<sub>(q2,doc2)</sub> = (0.478*0.076) + (0.6024\*0.787) + (0.469\*0.613) = 0.798
score<sub>(q2,doc3)</sub> = (0.478*0.595) + (0.469\*0.706) + (0.434\*0.383) = 0.782
The ranking would be doc2 > doc3 > doc1.


## Chapter 8:
### 8.1.)
Precision = 8 / 18 = 0.444
Recall = 8 / 20 = 0.4

### 8.4.)
At a recall level of 0, the interpolated precision is the highest that it can be for a higher recall level, so it can be between 0 and 1.

### 8.8.)
a) MAP<sub>1</sub> = AP<sub>1</sub> = (1 + 2/3 + 1/3 + 2/5)/4 = 3/5 = 0.6
MAP<sub>2</sub> = AP<sub>2</sub> = (1/2 + 2/5 + 1/2 + 4/7)/4 = 69/140 = 0.493
1 has a higher MAP.

b) It makes sense intuitively, since the relevant results in 1 are in the first places of the list. To get a good MAP, the first positions should have more relevant documents.

c) R-P<sub>1</sub> = 2/4 = 0.5
R-P<sub>2</sub> = 1/4 = 0.25
1 has a higher R-P, as well as MAP.

### 8.9.)
a) 6/20 = 0.3

b) 2*0.3\*(6/8) / (0.3+(6/8)) = 0.45/1.05 = 0.429

c) 100%

d) Max(3/9, 4/11, 5/15, 6/20) = 4/11 = 0.364

e) MAP = AP = (1 + 1 + 1/3 + 4/11 + 1/3 + 3/10)/6 = 0.555

f) MAP = AP = (1 + 1 + 1/3 + 4/11 + 1/3 + 3/10 + 7/21 + 8/22)/8 = 0.503

g) MAP = AP = (1 + 1 + 1/3 + 4/11 + 1/3 + 3/10 + 7/9999 + 8/10000)/8 = 0.416

h) 0.555 - 0.416 = 0.139