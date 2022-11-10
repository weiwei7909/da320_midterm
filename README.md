# DA320 Midterm Project

Midterm project for DA 320 - MongoDB Notebooks

In this project, I have two Jupyter notebooks. One Jupyter notebook collects data from Metacritic and stores it into MongoDB.  And another Jupyter notebook reads the data from MongoDB and did some transformation and analysis.

## Compare movies from one year against another

I compared the number of movies released each month between 2019 and 2020, we can see between March 2020 and June 2020, there were significantly fewer movies released. There was no surprise because that was when the pandemic started and there was lockdown, and many businesses were closed.

But the interesting thing was in December 2020, the number of movie releases was significantly more than that from December 2019. So I want to know which one is closer to normal, then next I plotted the month-by-month number of movies released averaged from 2000 - 2018.

## Compare movies with a keyword against movies with another keyword

I started out trying to find all the unique keywords and their occurrences in movie descriptions. Knowing some of the words like "the", "a" will be the most frequent, I also created an `excluded_list` to filter out these meaningless words.

I counted the occurrences of the unique words and listed the top 20 most common ones. From the list, I picked out the meaningless articles and propositions words and so forth, put them into the `excluded_list`, and run the logic again to add more to the `excluded_list`. I did this iteratively a few times until the top common words started to have some meanings.

What's interesting is that `his` and `her` were among the most popular, but judging from the occurences, `his` was a lot more common than `her`.  Notice here the word `her` has two meanings, the possessive word and also the objective word, so it is equivalent to `his` + `him`. And if we add the objective `him`, the count for the male countpart is even higher.

So now I am interested in seeing the occurrences of these words (and similar ones such as `man` vs `woman`) occurring in movie descriptions through the years to see if there are any trends.

To make the comparison meaningful, I combined some of the words together due to a single word taking on different forms/meanings (e.g. `her` is subjective and possessive, whereas `his` is possessive determiner and possessive pronoun). 

| Male term | Female term  |
|---        | ---          |
| he        | she          |
| him + his | her + hers   |
| man + men | woman + women|


From the graphs I got, we can see there was a big gap between the occurrences of male terms and these of female terms. The gap is especially large between the year of 2008 and somewhere around 2014.

I believe that is because in most movies, most of the lead characters are male, and that's why the description of the movie uses a lot of the male terms. But it is also observed that the female terms are in an increase trend, while the male terms are decreasing, starting somewhere around 2014 ~ 2016-ish. And in 2022, for the first time the occurrences of female terms are higher than these of the male terms.  I think this could be our society is become more aware of the gender bias, so there are more movies with female leads than before. Although slowly, the gap is getting smaller.

In the graph, we are using the word occurrences. One problem with that is a word could occurr multiple times in a movie description, and could throw-off the actual trend if a few movies with higher than usual word occurrences.I examined some statistics on word occurrences next to see if there were any outliers or some movies giving more weights than the rest.

From the boxplot I got, we can see each year, the distribution of these words in movie descriptions. There are a lot of "fliers" at the upper bound, because some movies have the words repeated many times in its description. This means using word occurrence count may not give the accurate picture as movies with repeated words are given more weight and therefore falsely inflates the count. So next,I checked the movie count instead, which means if a word shows up in a movie description, it is only counted as 1 occurrence, regardless how many times that word is repeated in the movie.

From the graphs, we are seeing the number of movies with these words in descriptions each year. The graphs show a trend very similar to the word occurrence graphs:

* There are more movies with male terms than these with female terms
* The gap became larger starting in 2007
* Sometime between 2014 ~ 2016, the gap is slowly closing
* The number of movies with female terms in description has been increasing
* In 2022 so far, the number of movies with female terms is just very slightly bigger than that with male terms.

These graphs give us more confidence about the trend. The counts are still not unique in this analysis because if different words occur in a movie's description, that movie will be counted as 1 for all these words. But this is okay because we are showing how many movies have these words, instead of how many words are showing in movie descriptions. If a movie description contains both a male term and a female term, that likely implies the movie has a male lead and a female lead; whereas if a male term repeats X times in a movie description and a female term repeats Y times in the description, it doesn't mean the movie has X number of male leads and Y number of female leads. So this data is more accurate and convincing.