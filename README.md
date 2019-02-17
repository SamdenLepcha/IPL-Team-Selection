# IPL-Team-Selection
The objective was to pick the likely best-performing eleven players using the data from the past IPL seasons. This repository showcases Data Wrangling, Feature Engineering and Data Visualisation. PCA was used to create a "ranking" variable based on the player's stats.  

<h2>These are the various methods used:</h2><br>
<h3>Feature Engineering</h3>
First of all, <b>we divided our dataset separately into batsmen, bowlers, wicket-keepers and all-rounders for each year<b>. This greatly helped us in further analysis and feature engineering. We keep all features that were originally provided in the dataset. However, since we divided our datasets separately into Batsmen, Bowlers, All Rounders and Wicket Keepers, we dropped irrelevant features in the respective datasets. For e.g., for Batsmen we dropped “Balls Bowled”, ‘Runs Conceded”, “Wickets Taken” and “Economy” and for Bowlers we dropped “Runs”, ‘Balls”, “Strike Rate”, “Four”, ‘Six”, “Highest Run”. For All Rounders we kept all features and for Wicket Keepers we dropped all the bowling attributes as stated above.<br>

However we also added some extra features which helped our dimensionality reduction technique which we used later in our approach to rank our players better. The features are as mentioned below:<br>

<b>Batting:</b>

<b>Hard Hitting Ability </b>= (4*Fours + 6*Sixes) / Balls Played by Batsman<br>

<b>Finisher</b> = Not Out innings / Total Innings played<br>

<b>Fast Scoring Ability</b> = Total Runs / Balls Played by Batsman<br>

<b>Running Between Wickets</b> = (Total Runs – (4*Fours + 6*Sixes))/(Total Balls Played – Boundary Balls)<br>
<br>

<b>Bowling:</b><br>

<b>Wicket Taking Ability</b> = Number of balls bowled / Wickets Taken<br>

<b>Consistency</b> = Runs Conceded / Wickets Taken<br>

For<b> All-Rounder</b> all the above features were added and for Wicket Keepers just the batting attribute were added.<br><br>

<h3>Ranking Players using PCA</h3>
Principal Component Analysis is widely used in applied multivariate data analysis for dimensionality reduction. Here, we use principal component analysis rank the cricket batsmen and bowlers who played in the Indian Premier League (IPL) competition. In particular, in our work, the first principal component is seen to explain a substantial portion of the variation in a linear combination of some commonly used measures of cricket prowess. The PCA was fit on the data after standardization. Below are examples of the 2018 dataset:<br>

<b>Batsmen:</b><br>
![image](https://user-images.githubusercontent.com/33536225/52917067-fab06880-330c-11e9-89e1-6a8cca6ba597.png)
Snapshot of 2018 Batsmen with 2 PCA components
<br>
<b>Variation in the data explained by the components:</b><br>
Component 1 = 14.82703404<br>
Component 2 = 7.38806297<br>
Thus we can see that Component 1 explains a greater part of the variation. Thus we use that as a Ranking Index to rank all the players.<br>
<b>Below is an example of the coefficients assigned by PCA to our features: </b>

  Component1/RankingIndex= 0.351Runs + 0.338Balls + 0.297StrikeRate + 0.338Fours + 0.324Sixes + 0.325HighestRunScored+ 0.200Ct_St+ 0.247RunOuts + 0.296MatchesPlayed + 0.265Hard Hitting + 0.297FastScoring + 0.02RunningBetweenWickets<br>
<b>Bowlers:</b><br>
![image](https://user-images.githubusercontent.com/33536225/52917089-46631200-330d-11e9-8363-174937693487.png)
Snapshot of 2018 Bowlers with 2 PCA components<br>

<b>Variation in the data explained by the components:</b><br>

Component 1 = 13.25160512<br>
Component 2 = 9.08744071<br>

Thus we can see that Component 1 explains a greater part of the variation. Thus we use that as a Ranking Index to rank all the players.<br>

<b>Below is an example of the coefficients assigned by PCA to our features:</b><br>

Component1/RankingIndex= 0.45589429BallsBowled + 0.43463612Runs Conceded + -0.22240624Economy + 0.45347261Wickets + 0.30987845Ct_St + 0.44498349MatchesPlayed +  -0.19604465Consistency + -0.12522551WicketTaking<br>


<b>Note: All the weights in negative imply that the lesser the better. For eg.- Economy</b><br>

<b>All-Rounders:</b><br>
![image](https://user-images.githubusercontent.com/33536225/52917118-af4a8a00-330d-11e9-9a6b-221b27d674ed.png) 
Snapshot of 2018 All-Rounders with 2 PCA components<br>

<b>Variation in the data explained by the components:</b><br>

Component 1 = 12.31900172<br>
Component 2 = 9.43282814<br>

Thus we can see that Component 1 explains a greater part of the variation. Thus we use that as a Ranking Index to rank all the players.<br>

<b>Below is an example of the coefficients assigned by PCA to our features:</b><br>

Component1/RankingIndex= 0.351Runs + 0.326Balls + 0.338StrikeRate + 0.297Fours + 0.338Sixes + 0.324HighesRunScored+ 0.200Ct_St+ 0.247RunOuts + 0.296MatchesPlayed + 0.265Hard Hitting + 0.297FastScoring + 0.02RunningBetweenWickets+ 0.45589429BallsBowled + 0.43463612Runs Conceded + -0.22240624Economy + 0.45347261Wickets + 0.30987845Ct_St + 0.44498349MatchesPlayed +  -0.19604465Consistency + -0.12522551WicketTaking<br>


<b>Note: All the weights in negative imply that the lesser the better. For eg.- Economy</b><br>



Similarly, in each year all the Batsmen, Wicket Keepers and Bowlers were ranked and all the players with a consistent rank (Note: consistent and not highest rank) throughout all the years were chosen with the constraints of the competition kept in mind.<br>


<b>Key Difficulties:</b><br>

Certain players did not play for a certain year, some players had one particular year where their performance dropped, some players stopped bowling/batting from particular years (though designated as All Rounders), and some players played in 2018 for the first time. However, our team was made taking into consideration the consistent performance of a player in all years between 2010-2018. Data previous to 2010 was not used because most players playing in 2019 never played in 2009 or earlier. We noticed that the data for 2010 and 2011 were actually the same and only considered one of them for our approach.
<br>
Data Wrangling:<br>

●	Same players across years have different formats of their names written. Some years have the First Name abbreviated while some do not.<br>
●	Player Type was not present in dataset before 2017.<br>

Both these problems had to be fixed before any further work/analysis.<br><br>

<h3>Resulting Team</h3><br>

Our playing 11 which we deduced from our PCA analysis:<br>

<b>1.	Batsmen:</b> Virat Kohli, Kane Williamson, Shikhar Dhawan, KL Rahul<br>
<b>2.	All Rounders:</b> Hardik Pandya, Shane Watson<br>
<b>3.	Bowlers:</b> Rashid Khan, Jasprit Bumrah, Bhuvneshwar Kumar, Sunil Narine,br>
<b>4.	Wicket Keeper:</b> MS Dhoni<br>

<b>Our choice of captain is MS Dhoni and Vice-Captain is Virat Kohli. </b><br>
Note: All the constraints were kept in mind during team formation.<br>
The PCA was done after the data was divided into batsmen, bowlers, wicket-keepers and all-rounders separately. Do keep that in mind while trying to run the code











