# Learning Equality challenge

<img height="300" alt="book-shelf2" src="https://user-images.githubusercontent.com/114782592/229075107-5d85c58a-41a1-49cb-b4ac-48a833080fbf.jpg">

The goal of this competition from Kaggle is to streamline the process of **matching educational content to specific topics** in a curriculum. To achieve that, an accurate and efficient model needs to be developed and trained on a library of K-12 educational materials that have been organized into a variety of topic taxonomies. 

These materials are in diverse languages, and cover a wide range of topics, particularly in STEM (Science, Technology, Engineering, and Mathematics).

The dataset presented is drawn from the Kolibri Studio curricular alignment tool, in which users can create their own channel, then build out a topic tree that represents a curriculum taxonomy or other hierarchical structure, and finally organize content items into these topics, by uploading their own content and/or importing existing materials from the Kolibri Content Library of Open Educational Resources. The leaf topic in this branch might then contain (be correlated with) a content item such as a video entitled Polar Coordinates.

## Objectives

The main objective of this challenge is to **predict which content items are best aligned to a given topic** in a topic tree, with the goal of matching the selections made by curricular experts and other users of the Kolibri Studio platform. In other words, your goal is to recommend content items to curators for potential inclusion in a topic, to reduce the time they spend searching for and discovering relevant content to consider including in each topic.

The evaluation function is the **mean F2 score**. The F2 score comes from a generalized form of F score in terms of 'beta':

![Fbeta](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQHnCTu8i1hATrd16s7HD8FXyU6z5JNdmNp971kzXUm7vJCkxq3)

when 'beta' = 2 we get the F2 score:

![F2score](https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcTL8nyvxGKVqzGEVO2q8xdNbHoExXsuoYDSunUK77eVwe4N0Wug)

The mean F2 score is obtained by calculating the F2 score for each topic and then calculating the mean value.

Read more about the challenge description [here](https://www.kaggle.com/competitions/learning-equality-curriculum-recommendations)

The full test set includes an additional 10,000 topics (none present in the training set) and a large number of additional content items. The additional content items are only correlated to test set topics.

![books1](https://user-images.githubusercontent.com/114782592/212356498-31846d32-4e1b-4cc0-b444-7b8c17802bb7.jpg)

# Results

This was my first Code Competition challenge, where you need to submit a notebook instead of a file with results. It was quite hard to troubleshoot a notebook running over an unknown dataset (testing dataset) and getting errors with vague descriptions. Especially because I wanted to create my own solution. In these sort of challenges, it is normal to start with a "benchmark" notebook, with a predesigned solution to get data and run a baseline model. Usually you can save a lot of time by not having to figure out how to deal with the dataset, and focus more on the model solution.

I was never able to get more than 0.252 of F2 scoring which led me to **rank #841 among 1,058 participants.** Actually the calculated score on my notebook was a bit higher than that, but I believe this is normal as you are not using the actual test dataset. I had to deal with RAM issues and optimize my solution by using Pandas in smarter ways. I've tried some solutions proposed by other participants, namely:

* A sentence transformer for semantic search
* A sentence transformer to calculate embeddings + KNN + LGBM
* A sentence transformer to calculate best matches + LGBM

The idea behind using more than one model type was to first make "blind" matches, then turning this problem into a binary classification one (match-no match) by checking which matches were "true" and which ones were "false".

My highest score came with the simplest solution, and using only a couple of columns from the dataset. Of course, not saying it was a **good** solution, just one that gave me the highest score I could manage. Anyway, at some point, I just wished to submit a sucessful notebook submission, and that I did manage.  

The goal of Code Competitions is to give some "fairness" among participants: the competition is more balanced, as all users have the same hardware allowances; and the winning models tend to be far simpler than the winning models in other competitions, as they must be made to run within the compute constraints imposed by the platform. Results are not artificially fabricated to get the best score on test data. It has to be through the code of a Kaggle notebook that will run the test dataset through a predictive model (or an ensemble of them).

# The Model

The most important features to be considered in this challenge are **text-based**: title, description and topic context (breadcrumbs). This requires feature engineering to work with the semantic information and chose the best matching text.

After attempting some models from SentenceTransformer, I ended up choosing a [retrieve-rerank solution](https://www.sbert.net/examples/applications/retrieve_rerank/README.html) for semantic search. I've used the pre-trained encoder "ST-all-MiniLM-L6-v2" and "ms-marco-MiniLM-L6" as cross encoder. I've 

Feature engineering was actually reduced to a minimum. I've decided to not use breadcrumbs afterall, and only clean text data for processing (remove ponctuation, white spaces, turn all text to lowercase). I processed the whole data grouping by language. I've tried the multilanguage pre-trained model (paraphrase-multilingual) but, again, score was worse.

# Eficiency Prize

This competition also had an Eficiency Prize. The idea was to have a predictive solution/model that could run only on CPU/RAM requirements. At some point, I've given up in finding a specific solution for this Efficiency Prize. Still, SentenceTransformer could run in CPU only, it just took longer. I thought that a model that takes some hours to match topics and contents is still much more effective than a team of humans doing the same.

Therefore, I've run my solution with GPU and without GPU. Running it without a GPU I was automatically applying for the Efficiency Prize. 

I want to highlight here that this was my second challenge participation and my first in a Code Competition. I had to do my best at making the code very lean in Python, working with a dataset I didn't even know the filename. It had to be "fool-proof" and validate each step instead of making assumptions. Only after applying these principles, I could get my sucessful submission. 

So, everything contributed to being in the leaderboard for the Efficiency Prize **ranking #32 among 107 participants.** Which was way better than the "normal" leaderboard. This does give some weight to me wishing to become a data engineer. :)
