# Search Intent Specificity Classifier

## Literature Review

1. [Gary Marchionini, _Exploratory Search: From Finding to Understanding_](https://dl.acm.org/doi/fullHtml/10.1145/1121949.1121979):
    - Lookup vs Exploratory (Learn + Investigate) Search [Diagram showing proposed model for identifying search intent specificity]
    - Lookup - _fast retrieval_ or _question answering_
    - Exploratory intent searches, may require strong human participation to support user with continuous & exploratoy process
    - Early techniques for relevance feedback for Exploratory Intent: 
        - asking for relevance feedback from users
        - _dynamic query_ interfaces (use mouse actions) - Dynamic Home Finder, SpotFire, TreeMaps, etc
    - __Relation Browser (RB)__ - facilitate exploration of the relationships  between  (among)  different  data  facets,  display alternative  partitions  of  the  database  with  mouse actions,  and  serve  as  an  alternative  to  existing search and  navigation  tools

***

2. [Doug Downey, Susan Dumais, Dan Liebling, Eric Horvitz, _Understanding the Relationship between Searchers’ Queries and Information Goals_](https://dl.acm.org/doi/abs/10.1145/1458082.1458143):
    - Describes how user behavior varies across _common_ & _rare_ search queries
    - Queries & URLs can be modeled using a _heavy-tailed Zipf distribution_
    - A user's query is often much more specific or general than  their  underlying  information  goal
    - Average  number  of  queries  the  user  must  execute  to satisfy  rare  goals  is  higher  than  for  common  goals
    - With increase in session depth, users  often  progress  from  frequent  to rarer  queries because:
        - specialization of query occurs more commonly than generalization
        - specialized queries become longer
        - longer queries are less frequent
    - Session begins with a search query and ends according to a subset  of  the  criteria  used  by  [White  and  Drucker](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/whitewww2007.pdf)
    - TaskDifficulty = - log<sub>2</sub>( P(goal URL) ) , where P(goal URL) = freq. of URL satisfying the user's gol, expressed as probability
    - Users  can  achieve  greater success in search if they utilize more general queries than their goal, and navigate to their goal page.

***

3. [Michael Bendersky, W. BruceCroft, _Analysis of Long Queries in a Large Scale Search Log_](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.323.7444&rep=rep1&type=pdf)
    - [TREC corpora](https://trec.nist.gov/data/kba.html) used for analysis
    - Why to study _long_ queries [5 <= len(query) <= 12]:
        - Better way to represent complex & specifc information  requirements
        - Existing retrieval methods perform worse for the long queries than for the short ones
    - Types of long queries:
        - Questions
        - Operators
        - Composite (composition of _short_ queries)
        - Non-Composite [Noun Phrase & Verb Phrase]
    - Users tend to click lower in the result list for the long queries than for the short ones
    - _Operator_ type queries have higher abandonment rate (due to Boolean nature)
    - _Question_ type queries have lower abandonment rate (users find partially plausible answers)

***

4. [Daniel Hienert, Matthew Mitsui, Philipp Mayr, Chirag Shah, Nicholas J. Belkin, _The Role of the Task Topic in  Web Search of Different Task Types_](https://arxiv.org/ftp/arxiv/papers/1808/1808.06813.pdf)
    - Large number of session variables defined based on _task type_ for experiment
    - Session variabes depend heavily on _task topic_, rather than simply  on _task type_.
    - _Topic familiarity_ had an overall weak effect on the _number of bookmarks_ and a nearly moderate effect on _query length_

***

5. [Emilie Palagi, Fabien Gandon, Raphaël Troncy, Alain Giboin, _A Survey of Definitions and Models of Exploratory Search_](http://www.eurecom.fr/en/publication/5165/download/data-publi-5165.pdf)
    - Exploratory searching behavior is similar to _information foraging_ (move from one information patch to another based on _infomration scent_) or _berrypicking_
    - Characteristics of exploratory search:
        - evolving search process & information need
        - several one-off pinpoints
        - multiple goals of search
        - multiple possible answers
        - anomalous state of knowledge (ASK) of user
        - open-ended search activity over time
        - multifaceted
    - __Marchionini’s model:__ Proposes a set of activities related to ES &   highlighted those associated to exploration(learn and investigate) or lookup.
    - __Ellis' model:__ Descries 6 major characteristics of information-seeking patterns in relation to retrieval systems

***

6. [Carolyn Theresa Hafernik, Bernard J. Jansen, _Understanding the Specificity of Web Search Queries_]()
    - 2 factors of specificity investigated:
        - part of speech
        - query length _[to validate the common belief that longer queries are more specific & to serve as a benchmark for testing additional factors]_
    - List of 9 attributes to identify query specificty as _narrow_:
        - URL
        - location with additional item
        - compares numtiple things
        - multiple distinct ideas _[potentially conflicting with previous paper]_
        - question with clear answer
        - request for directions, instructions & tips
        - specific date & additional items
        - number & additional items
        - name & additional items

***

7. [Bernard J. Jansen, Udo Pooch, _A review of Web searching studies and a framework for future research_](https://onlinelibrary.wiley.com/doi/epdf/10.1002/1097-4571%282000%299999%3A9999%3C%3A%3AAID-ASI1607%3E3.0.CO%3B2-F):
    - A _Web-searching study_ focuses on isolating searching characteristics of searchers using a Web IR system via analysis of data, typically gathered from transaction logs
    - Extensive review and analysis ofcurrent Web-searching studies
    -   | Category | Web Search | Traditional IR Search |
        | :---: | :---: | :---: |
        | Session length | 1-2 | 7-16 |
        | Query length | 2 | 6-9 |
        | Relevant documents viewed per session | <=10 | ~ 10 |
        | Use of advanced features | 9% | 9% |
        | Use of Boolean | 8% | 37% |
        | Failure rate | 10% | 17% |

***

8. [Kumaripaba Athukorala, Dorota Głowacka, Giulio Jacucci, Antti Oulasvirta, Jilles Vreeken, _Is Exploratory Search Different? A Comparison of Information Search Behavior for Exploratory and Lookup Tasks_](https://asistdl.onlinelibrary.wiley.com/doi/epdf/10.1002/asi.23617):
    - The most distinctive indicators that characterize exploratory search behaviors are query length, maximum scroll depth, & task completion time in _IR searching_
    - There are marked differences between web searching and searching with IR systems
    - Interface/Dataset used for expt: _arXiv_
    - Used results form statistical tests run after experiments to create a __Random forests classifier__ (with 10-fold cross validation) with the following features:
        - cumulative clicks
        - maximum scroll depth
        - query length
    - According to the classifier, the core lookup tasks are separable from the core exploratory tasks with nearly __85% accuracy__ & __0.859 AUC__ _[Assumed baseline as 50% accuracy & 0.5 AUC]_
    - Suggestions for future IR search interfaces
        - Exploratory tasks have greater scroll depths -> future search interface should show a longer list of items in the first SERP
        - search interface that automatically increases the snippet length for exploratory search task

***

9. [Anne Aula, Rehan M. Khan and Zhiwei Guan, _How does Search Behavior Change as Search Becomes More Difficult?_](https://www.researchgate.net/publication/221516065_How_does_Search_Behavior_Change_as_Search_Becomes_More_Difficult):
    - Rather than studying successful  strategies, here the focus is on failures (behavioral changes when having difficulty in finding   information)
    - Focus on _closed informational search task_
    - For unsuccessful tasks:
        - more question queries
        - advanced operators used often
        - longer time spent on search page
        - longest query somewhere in middle of search session
    - Other indicators of struggle for desired information:
        - scrolling up & down in a random fashion
        - revisiting pages they already visited

***

10. [Kumaripaba Athukorala, Antti Oulasvirta, Dorota Głowacka, Jilles Vreeken, Giulio Jacucci, _Narrow or Broad? Estimating Subjective Specificity in Exploratory Search_](https://eda.mmci.uni-saarland.de/pubs/2014/foraging-atukorala,oulasvirta,glowacka,vreeken,jaccuci.pdf):
    - Formalized a model that relies only on click data only to infer specificity of user queries 
    - Capturing _information gain_ [IG] (number of search results that a user clicks expressed as a function of the number of search results seen by the user)
    - _Seen-Clicked curve_: Logarithmic regression model with `g(n) = lambda * ln(n) - alpha`, where `g` is the effective information gain, `n` is the number of items seen, `lambda` & `alpha` are parameters to the model
    - `lambda` is dependent on 2 factors:
        - `lambda_u`: user-specific factor
        - `lambda_r`: results-specificity factor
    - Models obtained after experimentation:
      
      | Query Specificity | Model | Fit (R<sup>2</sup>) |
      | :---: | :---: | :---: |
      | Broad | 3.83 ln(n) - 3.59 | 0.97 |
      | Intermediate | 2.40 ln(n) - 2.06 | 0.97 |
      | Narrow | 2.05 ln(n) - 1.96 | 0.97 |

    -  Gradient of Seen–Clicked curve decreases (IG decreases) as the results become narrower for the user's information need
    - Also trained __C4.5 Desision tree__ (10-fold cross validation)
    - Achieved classification with __72.1% accuracy__ & __0.687 AUC__ [for broad vs narrow]
    - Achieved classification with __48.1% accuracy__ & __0.589 AUC__ [for broad vs narrow vs intermediate]
    - Potential applications of the model:
        - Adaptive IR systems
        - Personalized exploratory search systems
            - Query suggestions
            - Organizing information according to facets
            - Keyword prediction
            - Summarize results with possible visualizations
        - Substitute for relevance feedback technique

***

11. [Uchin Lee, Zhenyu Liu, Junghoo Cho, _Automatic Identification of User Goals in Web Search_](http://oak.cs.ucla.edu/~cho/papers/cho-usergoal.pdf):
    - Thee goal of a user can be classified into at least two categories: 
        - _Navigational_ (user has a particular Web page in mind and is primarily interested in visiting the page)
        - _Informational_ ( user does not have a particular page in mind or intends to visit multiple pages to learn about a topic)
    - Large fraction of queries can be associated with a particular goal that most users agree on
    - Most of the _unpredictable_ queries tend to belong to a few topic categories. A search engine can detect such queries using a topic detection method and treat them separately
    - Categories of features for the automatic identification of the user goal:
        - Past user-click behaviour:
            - click distribution: `Highly skewed => navigational`  &  `flat => informational`
            - avg. clicks per query: `low => navigational`
        - Anchor-Linkage Distribution:
            - `highly skewed towads rank 1 => navigational`
            - Practical concerns: _link spams_ & _mirror sites_
    - Benchmark Queries: 50 most popular queries issued to Google from the UCLA Computer Science Department
    - Using a classifier boundary `f = 1 * (median of click distribution) + 1 * (median of anchor-link distribution)` , __90%  accuracy__ is obtained

***

12. [In-Ho Kang, GilChang Kim, _Query Type Classification for Web Document Retrieval_](https://www.cs.cmu.edu/~ihkang97/papers/query_type.pdf):
    - User queries can be classified into 3 categories:
        - topic-relevance task [_informational_]
        - homepage finding task [_navigational_]
        - service finding task [_transactional_]
    - 3 types of information sources for web retrieval tasks:
        - Content information
        - Link information
        - URL information
    - URL information and Link information are good for the homepage finding task but bad for the topic relevance task
    - Different retrieval strategies are needed for different categories of queries
    - Dataset preparation for query classification task:
        - Training:
            - _TREC-2000 topic relevance task queries (topics 451-500)_ for Topic-relevance queries
            - _Queries for randomly selected 100 homepages_ for Homepage-finding task
            - Divided _WT10g_ into two sets, DB<sub>TOPIC</sub> and DB<sub>HOME</sub>: If URL type of document is _'root'_, add to DB<sub>HOME</sub>, else to DB<sub>TOPIC</sub>
        - Testing:
            - _TREC-2001 topic relevance task queries (Topic 501-550)_ for Topic-relevance queries
            - _TREC-2001 homepage finding task queries (1-145)_ for Homepage-finding task
    - Features for building query type classifier:
        - Distribution Difference of Query Terms
        - Mutual Information (to capture te semantic information between 2 frequently co-occuring words in a query)
        - Usage Rate as an Anchor Text (if query terms appear in titles and anchor texts frequently, this tells the category of a given query is the homepage finding task)
        - Part of Speech (topic-relevance tasks generally include verbs, while homepage-finding tasks usually have proper names)
    - Using all 4 features gave the best classification results, with __91.7% precision__ & __61.5% recall__ on the test sets

***

13. [Mauro Rojas Herrera, Edleno Silva de Moura a, Marco Cristo, Thomaz Philippe Silva, Altigran Soares da Silva, _Exploring features for the automatic identification of user goals in web search_]():
    - __Problem statement addressed:__ Given a set of n queries `Q = {q1; q2; ... ; qn}`, where each query `qi` is represented by a set of `m` features, i.e., `qi = {f1; f2; ... ; fm}` and a taxonomy, (a fixed set of `t` categories) `C = {c1; c2; ... ; ct}`, learn a classifier tha maps queries to their categories.
    - Taxanomies used:
        - C<sub>all</sub> = {_informational_, _transactional_, _navigational_}
        - C<sub>inf</sub> = {_informational_, _not informational_}
        - C<sub>tra</sub> = {_transactional_, _not transactional_}
        - C<sub>nav</sub> = {_navigational_, _not navigational_}
    - Learning algorithm: __Support vector machines (SVMs) with radial basis function__
    - Proposed features for Query representation:
        - Anchor text based features _(the distribution of occurrences of the query terms in anchor texts of pages is probably more skewed for navigational queries)_
            - Anchor Text Frequency Distribution 
            - Density of Domains in the top similar anchor texts _(compute the similarity of each anchor text to the query, take the top K answers and check whether the results are concentrated in a single domain or not)_
        - Page content based features
            - Density of Domains in the top similar texts _(Similar to the density of domains in the top similar anchor texts, but now using the full text of the documents)_ 
            - Titlemr _(take top 100 results, find ratio between the size of the largest substring of the query found in the page title and the size of the title itself & chose the largest such ratio)_
        - URL based features:
            - Match between query and domain
            - URLmr
        - Query based features:
            - Number of terms
            - Terms
        - Log-based features:
            - Query popularity _(number of occurrences of the query in the query log)_
    - Performance on experiments:
        - Much better best-case classification accuracies (82-90 %) across taxanomies on using best set of features from above on the  WT10g &  WBR03 collections
        - Navigational vs Informational classification:
            - SVM using all features __except__ terms, numer of terms, anchor text frequency , match b/w query & domain
            - __94.87 Precision__ & __94.87 Recall__
        - Navigational vs Informational vd Transactional classification:
            - SVM using all features __except__ terms, density of anchor domains, anchor text frequency , match b/w query & domain
            - __79.18 Precision__ & __79.18 Recall__

## Comments & Thoughts

- It would be good to explicitly mention that duration during which our data was collected & some specifics about the log files while writing about the Data Preparation
- It will be worth mentioning the differences between traditional IR systems & Web searching to highlight the segment that we are trying to address (web search).
- We can perhaps use the datasets mentioned in papers [12] & [13] above for testing our models as follows:
    - _Navigational (or homepage-finding)_ & _Transactional_ queries could be considered as _lookup_
    - _Informational (or topic-relevance)_ queries could be considered as _exploratory_

## Code [unreleased yet]