# qtm340_lightnovel-gender

## Background

The light novel is a popular literary genre in pop culture, especially in Japan. They are commonly illustrated in a manga art style, with anime-style covers and illustrations among pages of the story, and are often adapted into manga and anime. Individual volumes of light novels are short in length compared to ordinary novels, but one series of light novels can be made up of multiple volumes, where each volume is a different story under the same world setting, with in most cases different main characters and plots. 

Just like other Japanese subcultures, some light novels are considered to be having unethical or immoral content. For example, some might be accused of being sexually explicit or overtly violent. Light novels mostly target young people (age between 15-30), and the majority of the readers are related to some sub-culture such as anime, manga, or “otaku”. Light novels include a wide range of genres. One popular genre of light novels is fantasy and adventure in a different world. 

In this project, we are investigating whether there exist some characteristic patterns for female characters in those books. We hope to study the portrayal of female characters versus male characters in those light novels and how their powers evolve within the plot.

## Corpus

Our final corpus consists of the 56 novel series with a total of 290 volumes from 17 genres in English from [Baka-Tsuki translation community](https://www.baka-tsuki.org/project/index.php?title=Main_Page)

The original text data which is a subset of light novels under Language:English category from Baka-Tsuki are in [light_novel_original.zip](https://github.com/kristinagxy/qtm340_lightnovel-gender/blob/main/light_novel_original.zip).

The novel is included in our dataset if it meets two criterias. First, it needs to have at least one genre label with it. Second, it needs to have a complete English translation in a relatively standard format within the community website. 

Different volumes in the same novel series are treated as separate books. We also exclude the side stories. Besides, the translators might use different words when indicating a new volume. For example, most translators use the word “volume”, a small proportion of the translators use “phase” or “part”, while still some others simply use the title of the volume directly as an indicator. During the scraping process, we include all these different synonyms of volumes.

## Methods

### BookNLP

We use the Python package BookNLP to extract information about characters from the corpus we obtained. For our purpose, we use BookNLP to extract the proper references, referential gender, and actions for which the characters are the agent and patient. 

We first combine the chapters in each volume into a full-text by chapter order, and run BookNLP on the full-text for each volume in the corpus. BookNLP returns a JSON file with information about all characters in the book. Then we select the top 5 characters with high counts as the major characters, and our analysis will focus on these 5 characters. After that, we extract the information that we are interested in from the main characters, which are proper references and referential gender.

After collecting the basic information of the major characters, we further divide the volume into 5 parts with roughly equal number of words without breaking sentences in order to see how the power of characters evolves during the course of the story. Again we run BookNLP on the sub-parts of the volume. We obtain the information of the 5 main characters in each of the sub-parts by matching proper references. If the character in the sub-part is mentioned by at least one of the proper references of a main character, then the character is that main character. After locating the main characters, we extract the actions for which the character is the agent or the patient in that sub-part. Here the actions are verbs in the book. An agent is someone who performs the action, while a patient/theme receives the action. We would use this list of verbs to calculate the power score in the next section.

### Connotation Frames of Power

We employ the lexicon of power frames curated by Sap et al. in order to get the relative power for each of the major characters. In the lexicon, each verb has a corresponding label indicating whether it is the agent or the patient/theme of the verb that has more power, or the two have equal power. We first lemmatize the verbs in the lexicon and the list of verbs we have obtained for each character from BookNLP so that the verbs would match regardless of different conjugations. Then we compare the list of verbs for the characters with the lexicon. We determine whether the verb signals the character is having more power or less power by looking at the label of the verb in the lexicon and the relationship of the character to the verb. Then we decide whether we need to add or subtract one from the power score of the character.

Each character has an initial power score of zero. After we have gone through all the verbs, we normalized the power scores by dividing the current score by the total number of verbs in the list. In this way we take into account the differences in length and number of verbs of the novels. The final power score we obtain is a value from -1 to 1, with 1 indicating high power status, and -1 indicating low power status.

## Conclusion

Overall, the power of females is lower than that of males from the light novels that we incorporated in the dataset. The patterns vary based on the theme. According to the results, the action is the only theme where male characters have the dominant power over females since they are shown in general as more powerful from the beginning of the story till the end. In the mature and drama theme, though male characters are shown to be the powerful ones at the end, there are parts of the story where women appear to be more powerful. However, in the slice of life theme, though varying by part of the story, overall female characters have the dominant power over males. 

We suggest that the pattern are likely to be related to the target audience of the theme. In specific, the target readers for the theme “action” are mainly males, and they may prefer a more masculine plot that emphasizes men’s power and their capability as protectors. On the other hand,  the slice of life is a theme that refers to a naturalistic representation of real life, and it often combines romantic elements. The main characters are usually females and their high school friends, and the novels are often written from first-person perspectives. Therefore, the target audience of the theme mainly consists of female readers who expect to see characters of the same gender growing and thriving. In this way, it is plausible that female characters’ power is higher than males in light novels written in the slice of life genre. 



## The Notebooks

The notebook doing the scraping from Baka-Tsuki is in [340scraping.ipynb](https://github.com/kristinagxy/qtm340_lightnovel-gender/blob/main/340scraping.ipynb)

The notebook implementing the method on the corpus is in [340implementation.ipynb](https://github.com/kristinagxy/qtm340_lightnovel-gender/blob/main/340implementation.ipynb)

The notebook lemmatizing the power frame is in [Preparing_agency_power_lemma_csv.ipynb](https://github.com/kristinagxy/qtm340_lightnovel-gender/blob/main/Preparing_agency_power_lemma_csv.ipynb)

The dictionary containing information about the series is in [all_dict.pickle](https://github.com/kristinagxy/qtm340_lightnovel-gender/blob/main/all_dict.pickle)

The notebook integrating the dataframes and conducting the analysis is in [340getcsv_analysis.ipynb](https://github.com/kristinagxy/qtm340_lightnovel-gender/blob/main/340getcsv_analysis.ipynb)

The csv of the final information about the characters (name, gender, novel series, volume, genre, power in 5 parts) are stored in [power_normalized.csv](https://github.com/kristinagxy/qtm340_lightnovel-gender/blob/main/power_normalized.csv)

# Thank you!! 
