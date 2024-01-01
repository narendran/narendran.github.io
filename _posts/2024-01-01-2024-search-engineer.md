---
layout: post
comments: true
title:  "Search Engineer in 2024: Things to know"
category: "tech"
excerpt: "What should a search engineer know in 2024"
date:   2023-12-31 10:00:00
---

This blog is a living document, and I will continue to update it as I continue to learn more.

For a long-time now, I've found connecting people to the right information as truly meaningful and deeply energizing. Since I was in high school, I've loved organizing information and things and serving them to people in a way that they leave more knowledgeable and fulfilled -- more on this in a separate personal blog. I've recently realized that information search in companies like Google and Uber (where I've worked previously) is literally a planet-scale incarnation of the same theme and that is what drives me everyday to gain the skills and solve relevant, meaningful problems using those skills. Search is about **connecting a user’s <ins>verbalized intent</ins> (aka "query") to the <ins>information/product</ins> (aka "document")** that will fully satisfy their need. The goal of this article is to take this previous line, and unpack it component by component. Typical search systems have retrieval, query understanding and re-ranking.

## Retrieval

At the highest level of abstraction, search is about finding the documents which "match" the given query. This is technically called retrieval. There are typically two ways you can match a document based on the query.

* **Lexical Matching** is based on query and document having a lexical aka word/token level match. Conceptually, lexical matching needs a map of query-like tokens pointing to documents. So a document like *D1:"Dogs are animals"* would be 3 different mappings of *dog:D1, are:D1, animals:D1*. Now, a user query of "cat" would lead to no matches, while "dog" would retrieve D1 as a lexical match. In practice, we would have millions of documents and hence the map (or index) looks more like *dog:[D11, D13, D4, D9]* and order of linked documents under a token is typically based on document popularity.
* **Semantic Matching** involves augmenting the document with semantically matching tokens and indexing the document for those tokens as well. In the symbolic approach, we can add semantically relevant terms to the document (e.g. relevance feedback). With the wide adoption of neural networks, the more recent approach is to represent the document as a vector/embedding which captures the semantics of the full document, and we would use the same neural encoder to get the query embeddings. Then we would use nearest neighbour search algorithms to find the N closest document embeddings to the given query embedding. Semantic matching also help with precision since it naturally factors in the context in which the words occur e.g. "milk chocolate" vs. "chocolate milk".

Both matching techniques have their pros and cons: for instance, lexical matching works well irrespective of domain but has a fixed upper limit in terms of quality, and semantic matching brings in intelligence but its quality is limited by embedding quality (and transitively to the finetuning dataset size). If your domain has smaller sized queries and documents compared to web search, I would personally start with lexical matching first, and progressively add semantic retrieval as needed by the business. In more advanced deployments, we would see both retrieval strategies used simulataneously with a blending layer to merge the search results from both the retrieval strategies before going to re-ranking stage. 

Also, there are a few things which apply to both the retrieval paradigms: challenges with scaling up index sizes, live indexing, filters to skip documents (could be user-selected like time range or machine inferred like the query needs only "job" or "person" documents only), and there is a maximum limit on how many documents we want to match before considering retrieval done.

Things to know in 2024:
1. Hybrid retrieval techniques are getting widely implemented. E.g. Native support in [Apache Solr](https://sease.io/2023/12/hybrid-search-with-apache-solr.html), hybrid indexing in [Pinecone](https://www.pinecone.io/learn/hybrid-search-intro/). However, more commonly seen are custom solutions like Elastic Search for sparse + Vespa/Weaviate/Milvus/QDrant for dense retrieval. If there is a good overlap of candidates from both retrieval sources, then a classic, score-agnostic ranking technique called Reciprocal Ranking Fusion (RRF) also has proven to work very well. If you want to find a good middle ground: Staring with lexical matching and using Splade V2 for semantic expansion can take you a long way towards hybrid retrieval. Read up on the original [Splade](https://arxiv.org/pdf/2107.05720.pdf) technique.
2. Two-tower siamese networks continue to be the industry SOTA in building embeddings for embedding-based semantic retrieval. Graph embeddings, say for users/documents are used as input features on the document tower. E.g. [Personalized Retrieval in Etsy](https://arxiv.org/pdf/2306.04833.pdf)
3. LLM-based search experiences would be a step function capability in helping users. E.g. giving them [product reviews](https://arxiv.org/pdf/2308.04226.pdf), generating semantic tags for products, reducing the need for enterprises to build KG ontologies and maintain algorithms to convert unstructured information in the wild to map to their ontologies. Additionally, even with semantic retrieval, it is still non-trivial to answer questions like "healthy snacks for kids", "thanksgiving dinner ideas" etc. This is a place where LLMs can directly help.

## Query Understanding

Given that the user query comes from... humans, expect it to be imperfect and non-canonical. Once the query is corrected, we need to enrich it with information needed for effective retrieval. Following are some steps you could expect to see in a query understanding system.
* Spelling correction: Refer Symspell.
* Multi-lingual complexities: Handling tick signs in languages like Portuguese and Spanish (e.g. azúcar), normalizing queries from different Japanese writing systems.
* Compounding and decompounding
* Expansions
* Category classification: Many search systems today could retrieve results from multiple domains/verticals/categories.
* Entity classification: Person vs. Job Title, Food vs. Restaurant, Celebrity vs. Product etc.
* Named Entity Recognition: Segmenting the different parts of the query into different facets. E.g. "Naren who worked in Google" should be a Person entity search for the token "Naren" and employer facet being "Google".

Once done, we have corrected and enriched the query with a lot of metadata to help with both increasing the radius of retrieval (aka recall) and simultaneously scoping down to increase the relevance of results retrieved (aka precision).

Tools and Techniques to know in 2024:
* LLMs with their instruction following + world knowledge capabilities make excellent query understanders. Depending on the usecase, we could cache the query understanding result + run the LLM inference online for a different subset of queries. Note that we will have to run the same inferences on the document side as well to be able to match and boost.
* Rethinking eCommerce search to be done on unstructured, textual data instead of structured data. [Position paper](https://arxiv.org/pdf/2312.03217.pdf) by Instacart. However, I think relying on the LLM to generate product IDs is not a good idea, and we should expect inaccuracies.

## Re-ranking

The final step after query understanding and retrieval is deciding the final order of results to show to the user. This is usually an optional step, and typically needed to add a different preference order. For instance, in eCommerce search, the goal for both the user and the platform is for the user to purchase from the shop or purchase the item being shown, which means ranking based on probability of purchase, some combination of query-document relevance and ordering probability both work well. Typically, there is also filtering to remove away documents based on relevance conditions. Also, its not uncommon to have more than one re-ranking step.


Tools and Techniques to know in 2024:
* XGBoost models are continuing to be strong baselines, with deep learning models used to eke out the final few percentage points in NDCG.
* LLMs can help with evaluating ranking model performances, and also for generating relevance labels.

## Closing Thoughts

Finally, like in any real-world project, you would run into a ton of real-world idiosyncrasies, which you get progressively better at with more experience, like the following
1. Users usually prefer previously clicked documents (exact and similar). E.g. reordering same meal, preferring the same 2% fat milk product, preferring wikipedia for informational needs etc. So you might want to build that capability into all information surfaces. This is typically called **personalization**, and makes a significant improvement in user satisfaction especially in head/high-traffic queries.
2. In every layer and each component in that layer, we run into **coverage vs. quality tradeoffs** though in theory we need 100% on both. The choice in the tradeoff is highly dependent on the kind of product (ecommerce shopping, home assistant, information search results page, job search etc.), the kind of queries users are issuing on your platform and the number of documents we have to serve from.
3. While addressing the coverage vs. quality tradeoff, we inevitably run into machine learning solutions which come with their own complexities. In practice, its useful to have **override systems** which can be updated in real-time. This is usually implemented in a configuration language which takes effect without a server restart. E.g. the query classification ML model in your job search could classify "Naren" as a "Job Title" while in reality it should be "Person". Secondly, given that the rules of ML model are driven by real-world user data, it is important to have a continuous update and continuous monitoring setup for relevant models.
4. Once your information search surface gets popular, it becomes a good surface to show sponsored information related to the user and the user's intent -- and a precondition here is convincing ourselves that sponsored results are win-win-win for the sponsorer, the search platform and the user (to discover new products). However, remember that anything that is inserted in the middle of a relevance-ordered list would decrease user-perceived relevance, and hence its critical to continuously assess where we are in the tradeoff spectrum and adjust the triggering logic of sponsored items accordingly. Especially, its important to setup hold-out experiments to understand long-term effects of such changes.
5. Like any engineered product, there is a tradeoff between adding complexity vs. maintainability. But adding complexity is required to bring out magical user experiences. My advice here would be to keep adding complexity as needed and periodically assess the direction and perform simplifications.

Will keep adding more to this document as I keep learning. Please let me know if I am missing any other component here.

Thank you!
