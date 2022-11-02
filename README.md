# Gender and Power in Japanese Light Novels

## Abstract

In Japanese culture, the light novel – a combination of text and anime-style illustrations–is a relatively
new literary form. It derives from the broader otaku culture, which is also associated with video
games, manga, cosplay, anime, and other forms of Japanese popular culture. Though the light
novel lacks the global reach of some of these other genres, such as manga and anime, it nonetheless
attracts millions of readers across a range of gender and age groups. While distinct subgenres of
the light novel have emerged, such as romance, adventure, horror, and harem, issues of gender
stereotyping, power imbalances, and other forms of inequality remain strongly entrenched. These
issues can be attributed to how otaku culture is rooted in heterosexual male desire. This paper offers
a quantitative assessment of these issues of gender inequality. We analyze 290 light novels, scraped
from the Baka-Tsuki Translation Community Wiki, in terms of the power relationships between
female and male characters as they evolve over the course of each novel. We find patterns consistent
with issues of gender stereotyping and power differentials. More specifically, we find that female
characters consistently wield less power than male characters, especially towards the end of each
novel. We find some variation in specific subgenres. We conclude with close readings of two light
novels, demonstrating how a power frames approach to analyzing gender stereotypes in otaku culture
augments existing work on the subject.

## Corpus

Our final corpus consists of the 56 novel series with a total of 290 volumes from 17 genres in English from [Baka-Tsuki translation community](https://www.baka-tsuki.org/project/index.php?title=Main_Page)

When scraping the novels, we employed the following criteria for inclusion: first, it needed to have at least one genre label; and second, it needed to have a complete English translation in a relatively standard format.

The text data (after cleaning) which is a subset of light novels under Language:English category from Baka-Tsuki are in [light_novel_original.zip](https://github.com/kristinagxy/qtm340_lightnovel-gender/blob/main/light_novel_original.zip).

## Methods

### Main Character Identification

We picked the top 9 most frequently-mentioned characters as our focus of interest. The number was selected by finding the point with maximum curvature of normalized character mentions with respect to "frequency ranks".

### Main Character References and Referential Gender

We use the Python package [BookNLP](https://github.com/booknlp/booknlp) [^1] to extract the proper references, referential gender, actions for which the characters are the agent and patient as well as modifers and possessions of the character. 

We first run BookNLP on the full-text for each volume in the corpus. After collecting the basic information of the major characters, we then further divided each volume into 5 sections of equal length (without breaking sentences) to see the evolution of power in the story.

### Main Character Power Scores

We employ the lexicon of power frames curated by Sap et al. [^2] to determine the power score for each of the major characters. We normalized the power scores by dividing the score by the total number of verbs where the character is involved. The final power score we obtain is a value from -1 to 1, with 1 indicating high power status, and -1 indicating low power status.
 
 [^1]: D. Bamman, T. Underwood, N. A. Smith, A bayesian mixed effects model of literary character, in: Proceedings of the 52nd Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers), 2014, pp. 370–379.
 [^2]: M. Sap, M. C. Prasettio, A. Holtzman, H. Rashkin, Y. Choi, Connotation frames of power and agency in modern films, in: Proceedings of the 2017 conference on empirical methods in natural language processing, 2017, pp. 2329–2334.


## The Notebooks

The notebook doing the scraping from Baka-Tsuki is in [lightnovel_scraping.ipynb](https://github.com/kristinagxy/qtm340_lightnovel-gender/blob/main/lightnovel_scraping.ipynb)

The notebook implementing the method on the corpus is in [lightnovel_implementation_new.ipynb](https://github.com/kristinagxy/qtm340_lightnovel-gender/blob/main/lightnovel_implementation_new.ipynb)

The notebook lemmatizing the power frame is in [Preparing_agency_power_lemma_csv.ipynb](https://github.com/kristinagxy/qtm340_lightnovel-gender/blob/main/Preparing_agency_power_lemma_csv.ipynb)

The notebook describing the corpus, and conducting the visualizations and analysis of power scores is in [lightnovel_analysis.ipynb](https://github.com/kristinagxy/qtm340_lightnovel-gender/blob/main/lightnovel_analysis.ipynb)

The notebook conducting other analysis (modifiers and possessions) is in [lightnovel_other_analysis.ipynb](https://github.com/kristinagxy/qtm340_lightnovel-gender/blob/main/lightnovel_other_analysis.ipynb)

The notebook validating the power frames method is in [lightnovel_validation.ipynb](https://github.com/kristinagxy/qtm340_lightnovel-gender/blob/main/lightnovel_validation.ipynb)

## information about the series and the output dataframe

The dictionary containing information about the series is in [all_dict.pickle](https://github.com/kristinagxy/qtm340_lightnovel-gender/blob/main/all_dict.pickle)

The csv of total token counts and unique token counts for each volume is in [token_count.csv](https://github.com/kristinagxy/qtm340_lightnovel-gender/blob/main/token_count.csv)

The csv of the final information about the characters (name, gender, novel series, volume, genre, power in 5 parts) are stored in [output_1025.csv](https://github.com/kristinagxy/qtm340_lightnovel-gender/blob/main/output_1025.csv)


