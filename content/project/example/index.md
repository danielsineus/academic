---
date: "2022-18-08T00:00:00Z"
external_link: ""
image:
  caption: Photo by rawpixel on Unsplash
  focal_point: Smart
links:
- icon: twitter
  icon_pack: fab
  name: Follow
  url: https://twitter.com/DanielSineus
slides: example
summary: The codes to produce the results from the text titled " Quantitative Analysis of Four African-American Authors'books.
tags:
- Deep Learning
title: NLP Project on four authors
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
---

**SENTIMENT ANALYSIS TO STUDY SOME BLACK AFRICAN AMERICAN LEADERS**

**Objective**: *the primary aim of this paper is to present a correlation of the different* texts and the authors advocating the same cause. 

These authors are the following:

* W.E.B DUBOIS
* FREDERICK DOUGLAS
* ZORA NEALE HURSTON
* BOOKER T. WASHINGTON

 **The setting for the analysis**
 
The gutenbergr will be used to find the ID. Different ways of proceeding will be presented

```{r setu, include=TRUE, echo=TRUE}
library(gutenbergr) # We are supposed it was already installed
library(dplyr)
gutenberg_metadata%>%
  filter(title=="The Marrow of Tradition") #  Figure out the ID or the author of the book knowing the title of the book
```
As to the code above, it was just an example in case you know the title of book. But this is not the case in our study. 

Let's begin by looking for the ID of Douglas's books and download the books by ID

```{r seup, include=TRUE, echo=TRUE}
#In case we know the author's name and we would like to figure out the books published and which are stored in the gutenberg project.
gutenberg_works(author=="Douglass, Frederick")
fred_books<-gutenberg_download(c(23,99,202,31839,34915), meta_fields = "title")
```
```{r count, include=TRUE, echo=TRUE}
library(knitr)
kable(fred_books%>%
  count(title))
```


let's do the same for Booker T. Washington

```{r se, include=TRUE, echo=TRUE}
gutenberg_works(author=="Washington, Booker T.")
booker_books<-gutenberg_download(c(2376,26507,45125), meta_fields = "title")
head(booker_books)
```

Here comes the turn for Zora Neale Hurston 

```{r srte, include=TRUE, echo=TRUE}
library(stringr)
gutenberg_works(str_detect(author, "Hurston, Zora Neale"))
neale_books<-gutenberg_download(c(15902,19435,17187,22146), meta_fields = "title")
```

It is at last W.E.B's Du Bois's turn

```{r set, include=TRUE, echo=FALSE}
library(stringr)
dubois_books<-gutenberg_download(c(31254,15210,35399,15265,408), meta_fields = "title")
head(dubois_books)
```

Count numbers of words in each text or words per book 
For Dubois

```{r setup, include=TRUE, echo=TRUE}
library(knitr)
kable(dubois_books%>%
  count(title))
```
Count numbers of words in each text or words per book 
For Booker T. Washington
```{r ret, include=TRUE, echo=TRUE}
library(knitr)
kable(booker_books%>%
  count(title))
```
Count numbers of words in each text or words per book 
For Neale Hurston

```{r seti, include=TRUE, echo=TRUE}
library(knitr)
kable(neale_books%>%
  count(title))
```

Frequency for words for the books considered 
For Neale Hurston

```{r hurst, include=TRUE, echo=TRUE}
library(knitr)
library(tidytext)
str(neale_books)
book1<-neale_books%>%
  unnest_tokens(word, text)%>%
  anti_join(stop_words)
str(book1)
## Count words for Neale's books all together
n_book1<-book1%>%
  count(word,sort = TRUE)
kable(head(n_book1, 20))
```


```{r neal, include=TRUE, echo=TRUE}
library(knitr)
book3<-neale_books%>%
  unnest_tokens(word, text)%>%
  anti_join(stop_words)
str(book3)
## Count words for Neale's books all together
n_book<-book3%>%
  count(word,sort = TRUE)
head(n_book, 20)
```



```{r boook, include=FALSE, echo=TRUE}
str(booker_books)
book2<-booker_books%>%
  unnest_tokens(word, text)%>%
  anti_join(stop_words)
str(book2)
## Count words for Neale's books all together
bfd<-book2%>%
  count(word,sort = TRUE)
head(bfd, 20)
```



```{r dubois, include=FALSE, echo=TRUE}
book4<-dubois_books%>%
  unnest_tokens(word, text)%>%
  anti_join(stop_words)
str(book4)
web<-book4%>%
  count(word, sort = TRUE)
head(web,20)
book5<-fred_books%>%
  unnest_tokens(word,text)%>%
  anti_join(stop_words)
str(book5)
fd<-head(book5,20)
fred<-book5%>%
  count(word, sort=TRUE)
head(fred, 20)
```

Find the proportion of words per author and see their importance per author

```{r frequency, include=TRUE, echo=TRUE}
library(dplyr)
library(tidyverse)
library(tidyr)
freq<-bind_rows(mutate(bfd, author="Booker T. Washington"),
                mutate(fred, author="Frederick Douglass"),
                mutate(web, author="Du Bois"))%>%
  mutate(word=str_extract(word, "[a-z']+"))%>%
  count(author, word)%>%
  group_by(author)%>%
  mutate(proportion=(n/sum(n))*100)%>%
  select(-n)%>%
  spread(author, proportion)
freq<-drop_na(freq)
kable(head(freq,40))
colnames(freq)
head(esr)
wor<-freq%>%
  filter(word %in%c("abolition", "slavery","die", "hanged"))
wor
```




Sentiment Analysis for Booker T. Washington and W.E.B DUBOIS

```{r sentiment, include=TRUE, echo=TRUE}
library(dplyr)
library(stringr)
library(tidytext)
booker_books<-gutenberg_download(c(2376,26507,45125), meta_fields = "title")
head(booker_books)
tidy_book<-booker_books%>%
  group_by(title)%>%
  mutate(linenumber=row_number(),
         chapter=cumsum(str_detect(text, regex("^chapter [\\divxlc]",                                               ignore_case = TRUE))))%>%
  ungroup()%>%
  unnest_tokens(word,text)
head(tidy_book,40)
library(tidytext)
library(textdata)
lexicon_nrc()
get_sentiments("afinn")
get_sentiments("nrc")
get_sentiments("bing")
nrc_joy<-get_sentiments("nrc")%>%
  filter(sentiment=="joy")
nrc_joy
rec<-tidy_book%>%
  filter(title=="Up from Slavery: An Autobiography")%>%
  inner_join(nrc_joy)%>%
  count(word, sort = TRUE)
head(rec)
nrc_sad<-get_sentiments("nrc")%>%
  filter(sentiment=="sadness")
nrc_sad
sad<-tidy_book%>%
  filter(title=="Up from Slavery: An Autobiography")%>%
  inner_join(nrc_sad)%>%
  count(word, sort = TRUE)
head(sad)
#Get sentiment for Booker T. Washington
rec1<-tidy_book%>%
  filter(title=="The Future of the American Negro")%>%
  inner_join(nrc_joy)%>%
  count(word, sort=TRUE)
head(rec1) # At that time, while was a symbol of priviledge compared to black people
rec2<-tidy_book%>%
  filter(title=="The Future of the American Negro")%>%
  inner_join(nrc_sad)%>%
  count(word, sort=TRUE)
head(rec2,10)
 rec3<-tidy_book%>%
   filter(title=="The Story of Slavery")%>%
   inner_join(nrc_joy)%>%
   count(word, sort = TRUE)
head(rec3)
rec4<-tidy_book%>%
   filter(title=="The Story of Slavery")%>%
   inner_join(nrc_sad)%>%
   count(word, sort = TRUE)
head(rec4)
# frequency and total of words per book
book2<-booker_books%>%
  group_by(title)%>%
  unnest_tokens(word, text)%>%
  anti_join(stop_words)%>%
  count(word, sort = TRUE)
head(book2)
  
total_book2<-book2%>%
  group_by(title)%>%
  summarise(total=sum(n))
head(total_book2)
book_words<-left_join(book2, total_book2)
book_tdf<-fred_books%>%
  group_by(title)%>%
  unnest_tokens(word,text)%>%
  anti_join(stop_words)%>%
  count(word, sort = TRUE)
total_book_tdf<-book_tdf%>%
  group_by(title)%>%
  summarise(total=sum(n))
head(total_book_tdf)
book_words2<-left_join(book_tdf, total_book_tdf)
head(dubois)
bok_dubois<-dubois_books%>%
  group_by(title)%>%
  unnest_tokens(word, text)%>%
  anti_join(stop_words)%>%
  count(word, sort = TRUE)
head(bok_dubois)
bok_dubois_tdf<-bok_dubois%>%
  group_by(title)%>%
  summarise(total=sum(n))
bok_tdf<-left_join(bok_dubois, bok_dubois_tdf)


ter<-book_words%>%
  mutate(tot=(n/total)*100)
head(ter)
ter1<-ter%>%
  filter(title=="The Future of the American Negro"& n>50)
head(ter1)
#Sentiments for W.E.B DU Bois  
dubois<-dubois_books%>%
  group_by(title)%>%
  mutate(linenumber=row_number(),
         chapter=cumsum(str_detect(text, regex("^chapter [\\divxlc]",                                               ignore_case = TRUE))))%>%
  ungroup()%>%
  unnest_tokens(word,text)
tail(dubois)
rec5<-dubois%>%
  filter(title=="The Souls of Black Folk")%>%
  inner_join(nrc_joy)%>%
  count(word, sort = TRUE)
head(rec5,10)
rec5_1<-dubois%>%
  filter(title=="The Souls of Black Folk")%>%
  inner_join(nrc_sad)%>%
  count(word, sort = TRUE)
head(rec5_1)
rec6<-dubois%>%
  filter(title=="The Negro in the South\nHis Economic Progress in Relation to his Moral and Religious Development")%>%
  inner_join(nrc_joy)%>%
  count(word, sort = TRUE)
head(rec6,10)
rec6_1<-rec5<-dubois%>%
  filter(title=="The Negro in the South\nHis Economic Progress in Relation to his Moral and Religious Development")%>%
  inner_join(nrc_sad)%>%
  count(word, sort = TRUE)
head(rec6_1)
rec7_1<-rec5<-dubois%>%
  filter(title=="The Quest of the Silver Fleece: A Novel")%>%
  inner_join(nrc_sad)%>%
  count(word, sort = TRUE)
head(rec7_1)
rec7<-ec6_1<-rec5<-dubois%>%
  filter(title=="The Quest of the Silver Fleece: A Novel")%>%
  inner_join(nrc_joy)%>%
  count(word, sort = TRUE)
head(rec7)
neale_tidy<-neale_books%>%
  group_by(title)%>%
  mutate(linenumber=row_number(),
         chapter=cumsum(str_detect(text, regex("^chapter [\\divxlc]",ignore_case = TRUE))))%>%
  ungroup()%>%
  unnest_tokens(word, text)
head(neale_tidy)
bing_word<-neale_tidy%>%
  inner_join(get_sentiments("bing"))%>%
  count(word, sentiment,sort = TRUE)%>%
  ungroup()
head(bing_word)
plot_neal<-bing_word%>%
  group_by(sentiment)%>%
  top_n(30)%>%
  ungroup()%>%
  mutate(word=reorder(word, n))%>%
  ggplot(aes(word, n, fill=sentiment))+
  geom_col(show.legend = FALSE)+
  facet_wrap(~sentiment, scales = "free_y")+
  labs(y="Contribution to sentiment", x=NULL)+
  coord_flip()
plot_neal
ggsave(plot_neal, file="plot_neal.png", width = 5, height = 4, dpi = 100)

fred_douglass<-fred_books%>%
  group_by(title)%>%
  mutate(linenumber=row_number(), chapter=cumsum(str_detect(text, regex("^chapter [\\divxlc]",ignore_case = TRUE))))%>%
  ungroup()%>%
  unnest_tokens(word,text)
head(fred_douglass)
```

```{r sent, include=TRUE, echo=TRUE}
#get Sentiments for W.E.B Du Bois
dubois_sentiment<-dubois%>%
  inner_join(get_sentiments("bing"))%>%
  count(title, index=linenumber%/%80, sentiment)%>%
  spread(sentiment, n, fill = 0)%>%
  mutate(sentiment=positive-negative)
dubois_sentiment
library(ggplot2)
plot_dubois<-ggplot(dubois_sentiment, aes(index, sentiment, fill=title))+
  geom_col(show.legend = FALSE)+
  facet_wrap(~title, ncol=2, scales = "free_x")+
  labs(y="Contribution to sentiment in the texts of DU Bois", x=NULL)
ggsave(plot_dubois, file="plot_dubois.png", width = 5, height = 4, dpi = 100)

# Do the sentiment analysis for Booker T. Washington
Booker_sentiment<-tidy_book%>%
  inner_join(get_sentiments("nrc"))%>%
  count(title, index=linenumber%/%80, sentiment)%>%
  spread(sentiment, n, fill = 0)%>%
  mutate(sentiment=joy-sadness)%>%
  select(title,index, sentiment)
head(Booker_sentiment)
plot_book<-ggplot(Booker_sentiment, aes(index, sentiment, fill=title))+
  geom_col(show.legend = FALSE)+
  facet_wrap(~title, ncol = 2, scales = "free_x")+
  labs(x="Sentiments in the texts of Booker T. Washington", y=NULL)
plot_book
ggsave(plot_book, file="plot_book.png", width = 5,height = 4, dpi = 100)

booker_n<-tidy_book%>%
  inner_join(get_sentiments("bing"))%>%
  count(title, index=linenumber%/%80, sentiment)%>%
  spread(sentiment, n, fill = 0)%>%
  mutate(sentiment=positive-negative)
ggplot(booker_n, aes(index, sentiment, fill=title))+
  geom_col(show.legend = FALSE)+
  facet_wrap(~title, ncol = 2, scales = "free_x")
# Do the sentiment analysis for Frederick Douglass
fred_s<-fred_douglass%>%
  inner_join(get_sentiments("bing"))%>%
  count(title, index=linenumber%/%80, sentiment)%>%
  spread(sentiment, n, fill = 0)%>%
  mutate(sentiment=positive-negative)
plot_fred<-ggplot(fred_s, aes(index, sentiment, fill=title))+
  geom_col(show.legend = FALSE)+
  facet_wrap(~title, ncol = 2, scales = "free_x")+
  labs(x="Sentiments in the texts of Frederick", y=NULL)
plot_fred
ggsave(plot_fred,file="plot_fred.png", width = 5, height = 4, dpi = 100)
```




check the distribution for each novel

```{r distribution, include=TRUE, echo=TRUE}
book_words%>%
  ggplot(aes(n/total), fill=title)+
  geom_histogram(show.legend = FALSE)+
  xlim(NA, 0.0009)+
  facet_wrap(~title, ncol = 2, scales = "free_y")%>%
  na.omit()

```

Determine the most words used with wordcloud graph

```{r wordcloud, include=TRUE, echo=FALSE}
library(tm)
library(wordcloud)
library(reshape2)
library(ggplot2)
#Booker T. Washington

png("washington.png", width = 12, height = 8, units = "in", res = 300)
tidy_book%>%
  anti_join(stop_words)%>%
  count(word, sort = TRUE)%>%
  with(wordcloud(word, n, max.words = 120, main="Booker", rot.per = 0.35, colors = brewer.pal(8, "Dark2")))
dev.off()
#Booker for comparing positivity and negativity

png("bookerT.png", width = 12, height = 8, units = "in", res = 300)
tidy_book%>%
  inner_join(get_sentiments("bing"))%>%
  count(word, sentiment,sort = TRUE)%>%
  acast(word~sentiment, value.var = "n", fill=0)%>%
  comparison.cloud(colors = c("gray20", "blue"), max.words = 200)
dev.off()
#DUBOIS
png("dubois.png", width = 12, height = 8, units = "in", res = 300)
dubois%>%
  anti_join(stop_words)%>%
  count(word)%>%
  with(wordcloud(word, n, max.words = 120, rot.per = 0.35, colors = brewer.pal(8, "Dark2")))
dev.off()

png("WEBbois.png", width = 12, height = 8, units = "in", res = 300)
dubois%>%
  inner_join(get_sentiments("bing"))%>%
  count(word, sentiment,sort = TRUE)%>%
  acast(word~sentiment, value.var = "n", fill=0)%>%
  comparison.cloud(colors = c("gray20", "blue"), max.words = 120)

png("neale.png", width = 12, height = 8, units = "in", res = 300)
neale_tidy%>%
  anti_join(stop_words)%>%
  count(word)%>%
  with(wordcloud(word, n, max.words = 200, rot.per = 0.35, colors = brewer.pal(8, "Dark2")))
dev.off()
png("nealetidy.png", width = 12, height = 8, units = "in", res = 300)
neale_tidy%>%
  inner_join(get_sentiments("bing"))%>%
  count(word, sentiment,sort = TRUE)%>%
  acast(word~sentiment, value.var = "n", fill=0)%>%
  comparison.cloud(colors = c("gray20", "blue"), max.words = 200)
# Frederick Douglass 
png("douglass.png", width = 12, height = 8, units = "in", res = 300)
fred_douglass%>%
  anti_join(stop_words)%>%
  count(word)%>%
  with(wordcloud(word, n, max.words = 100, rot.per = 0.35, colors = brewer.pal(8, "Dark2")))
dev.off()
png("freddouglass.png", width = 12, height = 8, units = "in", res = 300)
fred_douglass%>%
  inner_join(get_sentiments("bing"))%>%
  count(word, sentiment,sort = TRUE)%>%
  acast(word~sentiment, value.var = "n", fill=0)%>%
  comparison.cloud(colors = c("gray20", "blue"), max.words = 200)
dev.off()
```



```{r zipf, include=TRUE, echo=TRUE}
 frequent_rank<-book_words%>%
  group_by(title)%>%
  mutate(rank=row_number(),termfrequency=n/total)%>%
  ggplot(aes(rank, termfrequency, color=title))+
  geom_line(size=1.1, alpha=0.8, show.legend = FALSE)+
  scale_x_log10()+
  scale_y_log10()
frequent_rank

# the bind_tf_idf function 
#determine the words that occur most in a collection of books per author
# For Booker T. Washington
head(book_words)
book_words1<-book_words%>%
  bind_tf_idf(title, word, n)

head(book_words1)
book_words1%>%
  arrange(desc(tf_idf))%>%
  mutate(word=factor(word, levels = rev(unique(word))))%>%
  group_by(title)%>%
  top_n(1)%>%
  ungroup()%>%
  ggplot(aes(word, tf_idf, fill=title))+
  geom_col(show.legend = FALSE)+
  labs(x=NULL, y="tf_idf")+
  facet_wrap(~title, ncol = 2, scales = "free")+
  coord_flip()

book_words1%>%
  select(-total)%>%
  arrange(desc(tf_idf))
book_word2_1<-book_words2%>%
  bind_tf_idf(title,word,n)

book_word2_1<-book_word2_1%>%
  select(-total)%>%
  arrange(desc(tf_idf))
head(book_word2_1)

book_word2_1%>%
  arrange(desc(tf_idf))%>%
  mutate(word=factor(word, levels = rev(unique(word))))%>%
  group_by(title)%>%
  top_n(1)%>%
  ungroup()%>%
  ggplot(aes(word, tf_idf, fill=title))+
  geom_col(show.legend = FALSE)+
  labs(x=NULL, y="tf_idf")+
  facet_wrap(~title, ncol = 2, scales = "free")+
  coord_flip()

bok_tdf1<-bok_tdf%>%
  bind_tf_idf(title, word,n)%>%
  select(-total)%>%
  arrange(desc(tf_idf))
head(bok_tdf1)

bok_tdf1%>%
  arrange(desc(tf_idf))%>%
  group_by(title)%>%
  top_n(15)%>%
  ungroup()%>%
  ggplot(aes(word, tf_idf, fill=title))+
  geom_col(show.legend = FALSE)+
  labs(x=NULL, y="tf_idf")+
  facet_wrap(~title, ncol = 2, scales = "free")+
  coord_flip()
```


 Word relationship
 
```{r relationship, include=TRUE, echo=TRUE}
# let's identify the parts of speech

fred_bigram<-fred_books%>%
  group_by(title)%>%
  unnest_tokens(bigram, text, token = "ngrams", n=2)%>%
  select(-gutenberg_id)%>%
  count(bigram, sort = TRUE)
head(fred_bigram)
resdr<-fred_bigram%>%
  separate(bigram, c("word1", "word2"), sep=" ")%>%
  filter(!word1%in%stop_words$word,
         !word2%in%stop_words$word)%>%
  count(title,word1,word2, sort = TRUE)
resdr_unite<-resdr%>%
  unite(bigram, word1,word2, sep=" ")
head(resdr_unite,20)
booker_bigram<-booker_books%>%
  group_by(title)%>%
  unnest_tokens(bigram, text, token = "ngrams", n=2)%>%
  select(-gutenberg_id)%>%
  count(bigram, sort = TRUE)

dubois_bigram<-dubois_books%>%
  group_by(title)%>%
  unnest_tokens(bigram,text, token = "ngrams", n=2)%>%
  select(-gutenberg_id)%>%
  count(bigram, sort=TRUE)
dubois_unite<-dubois_bigram%>%
  separate(bigram,  c("word1", "word2"), sep = " ")%>%
  filter(!word1 %in% stop_words$word,
         !word2 %in% stop_words$word)%>%
  count(title, word1,word2, sort = TRUE)%>%
  unite(bigram, word1,word2, sep = " ")
  head(dubois_bigram)
  
head(dubois_unite,20)
help("wordcloud")
```
