[Amazon Product Recommendation System](http://jmcauley.ucsd.edu/data/amazon/)
The Amazon product review datasets contains product reviews and metadata from Amazon, including 142.8 million reviews. We can build a recommendation system using possible tools like [SparkML ALS](https://spark.apache.org/docs/2.2.0/ml-collaborative-filtering.html)
- Read [recommendation system overview Chapter 9](http://infolab.stanford.edu/~ullman/mmds/ch9.pdf)
- Downloading the movies and TV dataset, read and explore it:
```bash
for line in open('Movies_and_TV_5.json','r'): 
     data.append(json.loads(line)) 
```
- Transform the json format into utility matrix table-alike data which contains: userid(row), itemid(col) and rating(values)
- EDA: exploratory data analysis: examine the sparseness of the data, very likely
large amount of less known items(movies) don't have ratings or very few ratings at all.
Plot a distribution of moving rating frequency on log scale, then filter out items that
have very few ratings since those ratings are highly sensitive to individual person preferences.
- Get familiar with the 3 common approaches, [an overview of recommendation system](http://datameetsmedia.com/an-overview-of-recommendation-systems/):
     - content based approach: utilizes a series of discrete characteristics of an item in order to recommend additional items with similar properties, we need to downloa the metadata of the movies to use this approach.
     - collaborative filtering approach:builds a model from a user’s past behaviors (items previously purchased or selected and/or numerical ratings given to those items) as well as similar decisions made by other users. [various implementations of collaborative filtering](https://towardsdatascience.com/various-implementations-of-collaborative-filtering-100385c6dfe0)
     - matrix factorization: state of art, using this approach won't need the data filtering preprocessing any more, the idea behind matrix factorization is to use latent factors to represent user preferences or movie topics in a much lower dimension space. With matrix factorization, less-known movies can have rich latent representations as much as popular movies have, which improves recommender’s ability to recommend less-known movies. recommended library, [pyspark ALS](https://spark.apache.org/docs/2.2.0/ml-collaborative-filtering.html)


Additional dataset:[recommendation dataset](https://www.kdnuggets.com/2016/02/nine-datasets-investigating-recommender-systems.html)


- Pyspark installation, credits to [it](https://blog.sicara.com/get-started-pyspark-jupyter-guide-tutorial-ae2fe84f594f)
1. Create a virtual environment ```python -m venv .venv/spark; source .venv/spark/bin/activate```
2. Install Java8 which is required to run Spark using brew: ```brew cask install homebrew/cask-versions/adoptopenjdk```
3. Install Spark using brew```brew install apache-spark```
4. Test to see if pyspark is installed by type ``pyspark``` in terminal
5. Add pyspark to jupyter notebook
 - 5.1 find the global profile for terminal, mostly it is ~/.bash_profile
- 5.2 ```vim ~/.bash_profile```
- 5.3 Press I to insert and paste the following codes in bash profile:
```export SPARK_PATH=~/spark-1.6.0-bin-hadoop2.6 
export PYSPARK_DRIVER_PYTHON="jupyter" 
export PYSPARK_DRIVER_PYTHON_OPTS="notebook" 
#For python 3, You have to add the line below or you will get an error
# export PYSPARK_PYTHON=python3
alias snotebook='$SPARK_PATH/bin/pyspark --master local[2]'
```
- 5.4 Exit vim: press ESC, and then enter :wq 
- 5.5 run ```source ~/.bash_profile``` to activate the setting
- 5.6 type pypark in terminal and it shall opens jupyter nobteook
