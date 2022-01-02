# Twitter-Follower-Followee-Relationship
We analyze the Twitter follower-followee relationships of two protests - #CAA NRC in India and #BlackLivesMatter in US.
Our aim is to study the digital spread of #BlackLivesMatter in the USA and #CAANRC in India. After collecting some data about the on-ground protests, we decided to use Twitter to study its online presence. We had to draw multiple network graphs to study how the support for the movement spread.

We divided the people involved with the protest into 4 groups:

the key protesters.
key politicians in power.
the key politicians in opposition.
celebrities and journalists.

We used the Twitter API using Tweepy in order to make a network graph to see what are the connections between these people. So we chose to look at the follower-followee relations between them.

Their twitter handles are saved in different list. This is done by passing an input string from the database, then split this string at each occurrence of @ An empty list is initialised then run two for loops, for say protesters and politicians. And for each pair of a protester and a politician, the code checks whether the first is following the next using the “show_friendship” tweepy function where we pass the source and target screen names. This returns a true or false and we append a row into the list with their handles and true/false result.

One of the issues that we faced is that since these were just Twitter handles, sometimes people either deactivate their account or they change their twitter handles so we used the try except feature so that the code keeps running even if it faces a user that doesn't exist. Since twitter has rate limits, which essentially means that there is a request window of 15 minutes and an upper cap limit on calls or requests you can make within this window. For example, for show_friendship it’s 180 requests per 15 minutes. Therefore, the code needs to run for a long duration thus we used the except tweepy.error.TweepError in case of non-existent handles. This happened with @DonaldTrump since his account was banned on Twitter.

After running the loops a list of lists is obtained. Using Pandas we create a dataframe with three columns: "Source", "Target" and “Follows”. And we convert this dataframe into a csv file and saved it.

Now, in order to display these relations diagramatically in a graph network we used Gephi and NetworkX. Import this csv file into Gephi under 'Edges' tab. Then based on this file edges are set between nodes if the follows column is true. Thus we get a directioned graph which represents how these key groups involved in the Black Lives Matter protests interacted on Twitter.

Gephi also allows other visual features like making the nodes different sized based on eigenvector centrality and displaying different colours and labels and their layouts. 
