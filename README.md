# food-recommender
Food Recommendation Data Science Project
-Jonathan Feng

### ABSTRACT

With the advent of data science dominating our markets the world has never been a better place. There exists a bit of data science in anything, from buying presents online to self-navigating cars and song recommendations. To make my point, data science has a dominating foothold in society and is too large to not leverage to any company’s advantage and in any industry. In this project we will be going through a series of steps applying machine learning and statistical techniques to create a food recommendation system based on a given food of choice by the user.

### INTRODUCTION

Recommendations are one of the unique applications of data science and can be applied to anything user based. As mentioned in class we have song recommenders and show recommenders. To give someone a grasp on how applied this is I can list out a handful of meaningful applications for recommendation systems (e.g., housing recommendations, stock purchases, any commercial site, and in our case specifically, recipe/food recommendations). To start off and preface this project I would like to give a brief rundown into the thought process behind this project.
To start off we are given a dataset that is filled with 39,774 different food recipes, each of them having their distinct unique id, the list of ingredients, and the cuisine type. With that given each of the list of ingredients comes in a string format that can be searchable by google to obtain that food. The food id does not specify what the searched-up food is, but it does provide a unique identifier for us to use later. From this data, we would like to generate a food recommender. Our output should be able to give a minimum of 3 recommendations of most similar foods given that our user chooses a unique id from that list from the start.

### PROCESS & RESULTS

Initially we are given two options on data, one that is pre-processed and one that is raw. The pre-processed data converts text to numbers which contains the weight of each word behind the search term. It is said that the order of words that are searched matters in Google search, so the weights will help in calculating the similarity later. For my study I will be going for the pre-processed data as the unprocessed one will take a little longer to make usable. With our data determined we would like to follow the guidelines highlighted in our goals section: recommending at least 3 foods to this customer, search them out in google, and visualizing our results.

![image](https://user-images.githubusercontent.com/34585038/147899683-ed5e01ce-54d6-4d6f-9c73-0143c5aed80d.png)

*Initial Pre-processed Data Format*

To recommend 3 foods we will have to go through a few processes, namely: cleaning our data and transforming it, performing PCA (Principal Component Analysis) for dimensionality reduction due to the sheer number of columns, using K-means to identify which food group belongs to what (seeing some results), and using a distance matrix to find the most similar foods associated with that item.

Going through the process, I was able to initially clean and id the dataframe. Furthermore, I performed PCA on 2 components to get a dimensionality reduction of the data and used that in the distance matrix later. 

![image](https://user-images.githubusercontent.com/34585038/147899726-0666a1af-215c-4290-842c-e290404d69b2.png)

*PCA Code Sample*

An elbow method was used to determine the number of optimal clusters based on inertia. Since it made a significant bend at the K=3 value I chose it as the fall off point and proceeded to perform a k-means clustering. The cluster itself yielded 3 groups of similar sizes, with centers relatively approximate to the center of each group. 

![image](https://user-images.githubusercontent.com/34585038/147899742-9d541456-1c31-4425-b8bb-6c9ee6d7b061.png)

![image](https://user-images.githubusercontent.com/34585038/147899745-9d12362b-73d5-4f7e-a98c-a35807315e69.png)

*Elbow Method Plot and Code*

As you can see the mint-colored group is elongated to the right a bit and should account for more variance in the PCA_1 group. For the grey and light green groups, we have some outliers in terms of PCA_2 towards the bottom and one singular outlier towards the top. The labels were then applied accordingly to their respective ids after this.

![image](https://user-images.githubusercontent.com/34585038/147899757-4aaaca1e-b0a6-4b6c-a369-ffbd2d53e1bb.png)

![image](https://user-images.githubusercontent.com/34585038/147899763-ec738439-e239-4919-9237-7f49ef5d3d21.png)

*K-means Plot Result and code*

After visually seeing the clusters, we can move on to generating our distance matrix, the distance matrix will provide information into how close each food is to each other in terms of the data generated from our PCA result. All tables and outputs will be in the index section but as you can see from that output, the lower the number the closer the foods are together.

![image](https://user-images.githubusercontent.com/34585038/147899783-577282a8-bc30-4af8-ab65-91ae77dadfa9.png)

*Distance Matrix Code*

![image](https://user-images.githubusercontent.com/34585038/147899786-9c20da7a-1049-44f3-b3cb-9c361621e37c.png)

*Distance Matrix Output*

Now that our results are all set, we can now generate the results. Although this was not required, I decided to have a bit of fun with making my own method for this part. In the food_recommender method I take a certain user input of a string of words like “Greek romaine lettuce cheese” and find the most similar thing to that by issuing a word count of how many of those words appear in each entry of our data. I then filter on max count to get a list of foods that are the most like what the user just entered and giving a random sample of 1 on that to get our initial sample to recommend on. I know we were supposed to choose an ID number but I decided to have a little fun with this so I could get a different result each time. With our initial result sampled, I use the distance matrix I generated earlier to find the top 3 foods that were most similar by accessing the index and filtering for the minimum distances since that is what indicates it being similar. My output generates 3 foods with the id, ingredients, and cuisine type.

![image](https://user-images.githubusercontent.com/34585038/147899808-1a9891d2-ce58-4001-a215-10ee446ffc65.png)

*Initial User Input*

![image](https://user-images.githubusercontent.com/34585038/147899818-86593b52-99b1-4d6d-b441-451ee9f3ad72.png)

*Recommendation Results*

Finally, we have our recommendations. The next steps to perform are a google search, visualization, and application of sorts. I decided to create another function that would query the results straight into googles search engine and return the results. I filtered for the first link that came up as that should be the recipe the id is referring to. Given the website I then further filtered the website for the name of the recipe itself and attempted to get a picture output. Although I was successful in grabbing the recipe name, sometimes the images vary with accuracy. I realize this may need quite a bit of work with data scraping and would need many conditions to account for how each page is built. Since this may not be too predictable, I will not be making any further improvements to it.

![image](https://user-images.githubusercontent.com/34585038/147899849-817dc77e-f816-44e1-9ffd-9c68c39aa0f3.png)

*Recommendation Search & Scraping Results*

### DISCUSSION
To briefly sum up our results, using the weighted data of the search terms behind the recipe id we were able to reduce the dimensions of the data, cluster them to see the general result our data fitted into, used the PCA data to form the distance matrix and drew recommendations based on those results. Our results were then fed into a more user centric function or that you would find in a usable application and shown the physical results in form of picture and name of the food. This in fact may be much simpler than what the industry example is, it highlights how easily we can perform such a task, and general useful insights from what otherwise would have thought to be “useless and unclean data” in the general public’s eye.

Overall, this has been an eye-opening project as we combine most of what we learned from class into somewhat of a full-fledged practical use case. If I were to add on to this project, I would implement somewhat of a robust testing system to make sure that our results were accurate, otherwise the other major thing I would like to add on is building out the application a bit more. For example, using our recommendation data, we can collect what a user likes/dislikes to build a certain profile. Then based on that profile we can even further narrow down our recommendations.


