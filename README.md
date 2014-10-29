TweetMaps
=========

6998 Assignment 1
============

Project Members:
Zissis Konstas (zk2178) , Farzaneh Motahari (fm2475)
=====================================================================================================

Project was done in eclipse.

This application displays a heatmap of geo-tagged tweets on a Google Map. The user has a the ability to select
tweets based on a keyword from a dropdown menu and see a visualization of their volume based on location.

The project is hosted on AWS. It is composed of a front-end and a back-end. The front-end (client-side code)is served to the user when he accesses the URL of the app. The back-end (server-side) lives on the server and is executed when the user makes a selection. More specifically:

The front end is composed of the following files:
-index.html (landing page)
-googlemaps.js (logic of front-end)
-styles.css and appstyle.css (stylesheets of the app)

The back end is composed of
-gettweets.jsp
-a relational database that is hosted on AWS containing the tweets data


The user selects a keyword in the front-end and then a request (through ajax) is made to the server (to the gettweets.jsp file) passing the selected keyword as a parameter in the url.

The server parsed the keyword and fetches the appropriate data from the Database which is saved in a mysql RDS Amazon Database. The returned data by the DB is saved in JSONobject and sent back to the client where the client extracts the coords from the JSONObjects and refreshes the heatmap according to the new data.

We used the python code attached (twitterstream.py) to download the tweets. It is a modified version of an available python resource for downloading tweets. We used the streaming API and filtered the returned JSON objects by track and language. As an example the url below looks for streaming tweets with keyword "ebola" and filters for English tweets.
"https://stream.twitter.com/1.1/statuses/filter.json?track=Ebola&language=en"

In the next step, we check to see whether the "coordinates" key of the JSON dictionary is not null and in such case, we extract the tweet_id, text, coordinates and timestamp of that query. Data of 300 such tweets are saved to the associated text files which is a tab delimited text file.

After we downloaded our 300 tweets per keyword, we connected to our DB in cloud via mysql terminal commands:
mysql -h <endpoint> -P <port> -u <username> -p <name of DB>

After inserting our password, through termina sql command, we created associated tables (for instance ebola) which has 4 columns (yweet_id, coordinate(ie lat,long), timestamp,text).

Then using the command:
LOAD DATA LOCAL INFILE '/path/ebola.txt' INTO TABLE ebola;
we populated the associated tables. After this step our DB is ready to be used by our application.

To run it locally, you can simply run it on your local host by opening the files as an eclipse dynamic AWS web project! You have to modify the serverUrl variable in googlemaps.js to point to your localhost. The only technology needed is eclipse and Tomcat installed.
