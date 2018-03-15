# Imitating Youtube features using Databases

This project uses three databases **MySQL**, **Neo4j** and **MongoDB** to create a Youtube-like application. 

The dataset is JSON files containing video data collected using Youtube API. The video features include the file name, tags, description and likes, comments, views etc.

## Databases

#### MongoDB
The most popular solution to store JSON documents in a database. The non-structed nature of JSON documents means that traditional RDBMS solutions using a structed schema fail. This calls for the need of a NoSQL database.

A python script is included that inserts the JSON documents into the MongoDB database.

```
$ python insert_mongo.py
```


#### Neo4j
The graph based database is used to store relationship between two videos. Each video is a node in the graph and edges are created based on the following :
* Two videos belonging to same channel.
* Two videos having similar tags. 
* Two videos having similar description.

The power of Neo4j lies in its ability to intuitively and efficiently store the relationships between entities in a database. If we were to model the same information in a traditional RDBMS then the number of tables and the processing overhead( a large no of joins to glean any insight) would perform very poorly in comparision.

A python file to create nodes and relationships is provided.
```
$ python insert_neo.py
```

#### MySQL
To store the user details, we use the MySQL database. Traditional RDBMS solutions work very well in scenarios where the data follows structured schema. This database stores the login details, video watch history, likes and subscriptions. 

---
## Backend

The backend of application is made in python using Flask. It has the following features:
* **Login**: Flask login module is for user authentication.
* **Trending Videos**: A video becomes more popular as it gets more views and likes. This module selects the most popular videos and shows them as suggestions. 
* **Word Correction**: A dictionary is created of unique words from database, and common english words. A Fuzzy logic based word correction algo is used to correct mis-spelled words in the application.
* **Channel Subscription**: Logged in Users can subscribe to a channel. It will be shown in user's start page and any new video by the channel will be highlighted.
* **User Home Page**: Each User has a home page where all his/her liked videos and subscribed channels are displayed.
*  **Channel Page**: Each channel has its own page where user can visit, subscribe and/or see the channel's videos. 
*  **Boolean Search Box**: An advanced search box with And, Or and not operations in search bar to ensure effective search.  
* **JavaScript powered UI**: The interactive web application makes the entire process smooth and user friendly.

### Pre-requisites
Install flask
```
$ pip install flask
```
Install flask_pymongo for MongoDB in flask
```
$ pip install flask_pymongo
```
Install flask_mysqldb for MySQL in flask
```
$ pip install flask_mysqldb
```
Install flask_login for Client Login 
```
$ pip install flask_login
```
Install py2neo for Neo4j
```
$ pip install py2neo
```
#### Run the application
Create a directory of words using: 
```
python directory.py
```
Create flask server to host the application using:
```
python search.py
```