# aws-mahout-recommender
AWS Mahout Recommender Demo

### Preparing the data set

```sh
wget http://files.grouplens.org/datasets/movielens/ml-1m.zip
unzip ml-1m.zip
cat ml-1m/ratings.dat | sed 's/::/,/g' | cut -f1-3 -d, > ratings.csv
```

### Moving data set to HDFS

```sh
hadoop fs -put ratings.csv /ratings.csv
```

### Running Mahout job

```sh
mahout recommenditembased --input /ratings.csv --output recommendations --numRecommendations 10 --outputPathForSimilarityMatrix similarity-matrix --similarityClassname SIMILARITY_COSINE
```

### View the results

```sh
hadoop fs -ls recommendations
hadoop fs -cat recommendations/part-r-00000 | head
```

### Installing the python packages

```sh
sudo pip3 install twisted klein redis
```

### Up redis server

```sh
wget http://download.redis.io/releases/redis-2.8.7.tar.gz
tar xzf redis-2.8.7.tar.gz
cd redis-2.8.7
make
./src/redis-server &
```

### Up web service with python

```sh
twistd -noy hello.py &
```

`hello.py` file is in this repo.

### Test

Open another terminal and run

```curl
curl localhost:8082/42
```

🔴🔴Remember to terminate all aws services once tutorial is done!!🔴🔴

### Resources

https://aws.amazon.com/blogs/big-data/building-a-recommender-with-apache-mahout-on-amazon-elastic-mapreduce-emr/
