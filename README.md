# News NLP Analysis

Exploratory natural language processing on 1,400 English news articles with spaCy and scikit-learn, written in Google Colab. University project. Notebook text and comments are in Serbian.

Notebook: [`news_nlp_analysis.ipynb`](news_nlp_analysis.ipynb)

## Steps

1. **Preprocessing.** Lowercasing, regex cleanup, lemmatization with spaCy `en_core_web_sm` and removal of stop words and punctuation.
2. **Named entity recognition** on the original (uncleaned) text. Entity counts by type (28,830 people, 22,917 organizations, 15,158 places…) and the most frequent entities per type.
3. **Rule-based matching.** Three spaCy `Matcher` rules: market movements such as "shares fell" (3,153 matches), news dates (4,462) and official positions (292).
4. **Bag of words and bigrams.** The most frequent words and bigrams with `CountVectorizer`, shown as bar charts.
5. **Similarity.** Word and sentence similarity with the `en_core_web_md` word vectors: "shares"–"stocks" 0.46 vs "shares"–"police" 0.05, and 0.47 vs 0.29 for a pair of sentences on the same topic vs a different topic.

The notebook ends with a short conclusion: the sample is dominated by US politics around the 2016 election, with Trump, Clinton and Obama as the most mentioned people.

## Data

The dataset (`newsSourcesSAMPLED100.csv`, columns: source, author, title, text, date) was provided with the course and is not in this repository.

## Running

Open the notebook in Colab with `https://colab.research.google.com/github/veljko-milisavljevic/news-nlp-analysis/blob/main/news_nlp_analysis.ipynb` and upload the CSV, or run it locally:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python -m spacy download en_core_web_sm
jupyter notebook
```

The notebook downloads `en_core_web_md` itself in step 5.

## Known limitations

- The small spaCy model often labels "Trump" as an organization (2,329 times, more often than as a person: 1,587), so the counts per entity type are approximate.
- The `Matcher` counts overlapping matches, and one market rule allows any number of tokens between the noun and the verb, so the match counts are higher than the number of distinct phrases.
- The news-date rule lists only some months (January, February and August–December).
- Similarity scores from averaged word vectors are a rough measure of topic, not of meaning.

## License

Code is under the [MIT License](LICENSE). The articles belong to their publishers.
