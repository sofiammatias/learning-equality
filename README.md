# Learning Equality challenge

<img height="300" alt="book-shelf2" src="https://user-images.githubusercontent.com/114782592/229075107-5d85c58a-41a1-49cb-b4ac-48a833080fbf.jpg">

The goal of this competition from Kaggle is to streamline the process of **matching educational content to specific topics** in a curriculum. To achieve that, an accurate and efficient model needs to be developed and trained on a library of K-12 educational materials that have been organized into a variety of topic taxonomies. 

These materials are in diverse languages, and cover a wide range of topics, particularly in STEM (Science, Technology, Engineering, and Mathematics).

The dataset presented is drawn from the Kolibri Studio curricular alignment tool, in which users can create their own channel, then build out a topic tree that represents a curriculum taxonomy or other hierarchical structure, and finally organize content items into these topics, by uploading their own content and/or importing existing materials from the Kolibri Content Library of Open Educational Resources. The leaf topic in this branch might then contain (be correlated with) a content item such as a video entitled Polar Coordinates.

The goal is to **predict which content items are best aligned to a given topic** in a topic tree, with the goal of matching the selections made by curricular experts and other users of the Kolibri Studio platform. In other words, your goal is to recommend content items to curators for potential inclusion in a topic, to reduce the time they spend searching for and discovering relevant content to consider including in each topic.

Read more about the challenge description [here](https://www.kaggle.com/competitions/learning-equality-curriculum-recommendations)

**Ranked #841 among 1,058 participants.**


The full test set includes an additional 10,000 topics (none present in the training set) and a large number of additional content items. The additional content items are only correlated to test set topics.

![books1](https://user-images.githubusercontent.com/114782592/212356498-31846d32-4e1b-4cc0-b444-7b8c17802bb7.jpg)

# Efficiency Prize

There is an Efficiency Prize I wish to compete in. It focuses on model efficiency, since highly accurate models are often computationally heavy. 
Such models have a stronger carbon footprint and frequently prove difficult to utilize in real-world educational contexts. 
These models aim to help educational organizations, which have limited computational capabilities.

Personally, I find this challenge even more interesting than the simple "get best score possible" for this problem, as it requires to balance best performance with low computational capability (actually, the equivalent to my own pc😁 )  

# The Model

__on-going work__

The most important features to be considered in this challenge are **text-based**: title, description and topic context (breadcrumbs). This requires feature engineering to work with the semantis information and chose the best matching text.
SentenceTransformer LERC model has been chosen by some of the competition teams. However, as this requires a GPU it's going only to be one of the possibilities in my solution.
I aim to explore other NPL models for this feature engineering as well as simple tokenizers and see how the model predictions scores.



