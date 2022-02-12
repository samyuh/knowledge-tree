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