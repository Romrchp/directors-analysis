# Frames of success :  Diving into the minds of movie wizards

## A Data Story of the project, detailing our work and results is available [here!](https://epfl-ada.github.io/ada-2023-project-crunchychicken/)

#### The data used for the project is downloadable [here](https://drive.google.com/drive/folders/1MjRoBM-AJgTZPzMtvTxL-H9mFcC2Ld6P?usp=sharing)

## Abstract

Stanley Kubrick is known to have at least one great movie in every major movie genre. Conversely, when you see David Fincher's name as the director of a new movie, you are almost sure that there is going to be one or more serial killers involved. The directorial approach of the most successful directors can be so different and taking the right directorial approaches early can lead a director to achieve significant success in their career, and is believed to be the main factor determining the quality of the movie. In this data analysis project, we will utilize the CMU Movie Summary Corpus, along with supplementary datasets, to examine approaches of the brightest directors from three angles: the genre of their films, the team surrounding them, and the character personas in their movies. We aim to gain a clear insight on how their decisions impact the overall success of the movie.


## Research Questions 

To adress and quantify the director's decisions consequences on their movies, we decided to focus on three major research questions :

1. **How impactful is the team surrounding the director on the success of the movie?**

    Are the directors who always work with the same crew more successful? Successful directors built up their renown across the industry thanks to now very popular movies, but can it also be thanks to the presence of certain individuals in their team? If yes, how frequently have they been collaborating with each other?
    Are some directors successful only because they cast popular actors?

2. **To what extent does the director's choice of movie genre affect the success of the movie?**

    Are more successful directors more often specialized in a certain combination of genres? Are directors who tend to work on more diverse projects less successful? Is there a correlation between a director's critical success and the evolution of their style, regarding the choices of movie genres? To what extent do directors experiment with new genres and thematics over the course of their career, and is there a pattern of periods of experimentation followed by periods of consistency?

3. **What is the impact of the director's character choices on the success of the movie?**

    What types of characters do successful directors choose? How diverse the directors are in their character choices? Can we find very successful directors that always use the same type of characters or others that vary a lot in their personas choices? In definitive, how does this impact the movie's success?


## Description of the Datasets used

### CMU Movie Summary Corpus

The dataset is available online [here](https://www.cs.cmu.edu/~ark/personas).
The CMU Movie Summary Corpus is the basis dataset we were provided with and asked to work with for this project. It contains ~40k movie summaries extracted directly from Wikipedia as well as their metadata (such as Title, Revenue, Runtime, Genre...) aligned with Freebase. It therefore allowed us to establish a basis of both what we needed and already had to answer our questions. More specifically, this dataset does not contain information about directors, which is why we completed the information it contains with other datasets (see next sections)

### Stanford CoreNLP-processed summaries
The dataset is available online [here](https://www.cs.cmu.edu/~ark/personas/data/corenlp_plot_summaries.tar).
By using this dataset access to structured and rich data, which will help to understand the nuances of movies, characters and directorial style. We can accurately identify the characters, their actions and attributes, allowing to categorize them based on their traits. The type of characters and their dynamic will give key insights on directors narrative styles. 


### IMDb Non commercial datasets
The dataset is available online [here](https://developer.imdb.com/non-commercial-datasets/). Using this dataset, we can enrich the metadata about the movies in the CMU dataset, as well as the cast and crew of a movie. The major challenge for using this dataset is merging it with the CMU dataset. We have been able to merge them successfully by crawling Wikipedia and querying Wikidata to get the corresponding IMDb movie ID for each movie present in the CMU dataset. Next step is to also find such a mapping between the actors and actresses in the CMU dataset and their corresponding ID in the IMDb dataset, which is less critical.

### 'TheMovies' Dataset

The dataset is available on [Kaggle](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset?select=movies_metadata.csv). This dataset contains metadata for all 45,000 movies listed in the Full MovieLens Dataset. In it, we retrieve some interesting information to cure as well as enrich our CMU concerning the movie runtimes, release years, production companies, as well as precious information regarding the movie's success, with some ratings and the revenue. In the dataset, 27 500~ movies are also part of our CMU Movie Corpus.

## Metrics 

In order to be able to quantify the impact of the directors on their movies and thus answer our research questions, we of course need to precisely define our perception of both movie & directors success.

### Success through popularity of a movie
In this study, we mainly study the success of a movie through the prism of its popularity. We integrate both popularity and quality of the movie by defining a success score, $$S_{movie} = {Rating}_{movie} \times \log({Votes}_{movie})$$. The effectiveness of this metric was assessed by the very good matching of movies with a high home-made success score with the number of awards won by the movie. In addition, this allows to not overcomplicate the operations and have a representative metric of a movie's success.

### Success and popularity of a director
Taking Martin Scorsese for instance, movies like Casino, Goodfellas, and Taxi Driver are enough to make him a successful director, and for such directors, we should get a *success score* close to maximum, so why impinging his score with taking into account the success of movies like Made in Milan or The Family which nobody knows about? It is following this idea that we decided to use, for each director, the average of its most successful movies as a measure of a director's success. The main metric used is the 'avg-3' score, based on the 3 most successful movies of the director, which yielded good results. We also defined 'avg-5' and 'avg-10' scores, that were used in some of the analyzes depending on the aim of the latter.

# Methods 

## Data preprocessing

A huge emphasis has been made on data preprocessing in order to make the data usable for our research questions. The main common step to all research question were made through the building of helper files (in `/helpers`) that 1) Loaded the data correctly from the different .csv and/or .tsv files from CMU, IMDb and other sources used, as well as 2) an extensive pre-cleaning of the data. This comports correct renamings of the various dataframes columns, extensive pre-cleaning of bad data types and overall the establishment of a suitable work environment.

## Research Question 1 
Research question 1 was focused on the impact of the crew of the movie on the director's and by extension the movie's success. Correlational analyses were mainly used throughout the question, including statistical t-tests as well as Tukey's HSD and dataset matching for potential cofounders, to look at the impact of the crew size and of the particular core members (using an overlap coefficient metric as well). Using a pre-built dictionnary containing all connections between directors and their crew members, bipartite graphs were built for both actors/actresses only & all crew members. The bipartite projections obtained from the latter on the director's nodes were then analyzed, to assess the amount with which 1) successful directors share actors/actresses-only collaborations and 2) successful directors plainly share all types or relations in order to compare both phenomenon. 

## Research Question 2

Research question 2 looks at the impact of directors' genre selection on the success of their films. The research involves a comprehensive analysis of the interaction between genre, project diversity and the evolution of directors' styles, using both statistical analysis and graphical representation. By looking closely at directors' careers, we seek to discern patterns in their genre choices and their correlation with the overall success of their films.

## Research Question 3
Distributions were studied with regard to the director score, the character type & choice as well as the relationship between the movie score & the character type. To quantify diversity, the main metric used was the Shannon Diversity index, to efficiently assess the diversity of directors in terms of all the elements previously cited. A regression model was also established to quantify the director's succes with respect to its choices, and datasets were matched for potential cofounding factors accordingly.

### Q3 specific : Natural Language Processing
For Question 3 specifically, following [*Learning Latent Personas of Film Characters*](https://www.cs.cmu.edu/~dbamman/pubs/pdf/bamman+oconnor+smith.acl13.pdf), from the NLP data of movie summaries, we extract characters. For each character, we find the associated dependency of type: agent, patient, attribute. Then, we generate bags of words and do LDA to get the latent personas.


## Repository Structure 
- 📂 `data` : Folder containing the different datasets described earlier and used for the project. Subfolders here are the different datasets, i.e `CMU`,`IMDb` & `MovieLens`

- 📂 `generated` : Contains the different files generated by our code, mainly the mappings used for data curation as well as in annotations useful for NLP & Question 3. Necessary for the running of Q1, Q2 and Q3 notebooks.

- 📂 [pipelines](pipelines/) : Contains the pipelines files, useful for the NLP part of Q3. 

- 📂 `helpers` : Helper Python files for the different parts of our project
    - 📄 `external.py`: Performs the mapping being movies in our dataset and the information available on Wikipedia.
    - 📄 `readers.py`: Treats raw data to curate, clean and load the latter properly for further data exploration and analysis.
    - 📄 `utils.py`: All small adjustments & preprocessing utility functions

- 📒 `Q1.ipynb` : All work related directly to answering the first research question. Contains results present in the data story, as well as additional work.

- 📒 `Q2.ipynb` : Same, but for Q2.

- 📒 `Q3.ipynb` : Same, but for Q3.

## Run Instructions

To obtain and display the results present in the data story, you should have stored all data & necessary preprocessed files in the three 📂 [generated](generated/), [data](data/) & [pipelines](pipelines/).

Then, running the three Q1, Q2 and Q3 notebooks should yield the results obtained in the data story. Some cells take ~30 minutes to run, the total running time should be of 2-3 hours on a standard machine.


## Authors

**Advanced Data Science (CS-401) 2023**

- [Chang Chun-Tzu](mailto:chun-tzu.chang@epfl.ch)
- [Arthur Lamour](mailto:arthur.lamour@epfl.ch) 
- [Clémence Mayaux](mailto:clemence.mayaux@epfl.ch) 
- [Sepehr Mousavi](mailto:sepehr.mousavi@epfl.ch) 
- [Romain Rochepeau](mailto:romain.rochepeau@epfl.ch) 
