me'23\s.*\s.*\s2013' book_tweets.tsv data
cd data
wget www.derekruths.com/static/reading_tweets/books_tweets100000.txt.gz
gunzip books_tweets100000.txt.gz
cd ..

awk -F '"text"' '{print $2 }'  data/books_tweets100000.txt | awk -F '"' '{print $2}' > text
awk -F '"created_at"' '{print $2 }'  data/books_tweets100000.txt | awk -F '"' '{print $2}' > date
awk -F '"lang"' '{print $2 }'  data/books_tweets100000.txt | awk -F '"' '{print $2}' > lang
awk -F '"id":' '{print $2 }'  data/books_tweets100000.txt | awk -F ',' '{print $1}' > id
sed -i 's/[^0-9]*//g' id
paste id date lang text > book_tweets.tsv
rm text date lang id
grep 'Oct 23\s.*\s.*\s2013' book_tweets.tsv> tweetsOct2012.tsv
grep '#gameofthrones' book_tweets.tsv > tweets_got.tsv

touch temp_text
echo 'The number of russian tweets is:' > temp_text
echo 'The number of tweets from Aug 2016 are:' >> temp_text
echo 'The number of tweets containing a retweet is:' >> temp_text
echo 'The number of tweets mentioning game of thrones is:' >> temp_text

touch res
grep '.*\t.*\tru' book_tweets.tsv | wc -l > res
grep 'Aug\s.*\s.*\s.*\s2016' book_tweets.tsv | wc -l>> res
grep '.*\t.*\t.*\tRT.*' book_tweets.tsv | wc -l>>res
wc -l < tweets_got.tsv >> res

paste temp_text res > results.txt
rm res temp_text
