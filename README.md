![intro image](images/NFL-first-page.jpg)

[The Data](#The-Data)

- [QuickDBD](#QuickDBD)

[Features](#Features)

[Newly Created Features](#Newly-Created-Features)

[Cumulative Averages - described](#Cumulative-Averages---described)

[Cumulative Averages - example](#Cumulative-Averages---example)

[MatPlotLib Visualization - the field and positions](#MatPlotLib-Visualization---the-field-and-positions)

[Correlations](#Correlations)

[The Training](#The-Training)

- [Random Forest - Feature Importance](#Random-Forest---Feature-Importance)
 
- [KNN](#KNN)
 
- [Deep Model - Keras/TensorFlow](#Deep-Model---Keras/TensorFlow)
 
[Increasing the Volume of Data Over 9 Weeks](#Increasing-the-Volume-of-Data-Over-9-Weeks)

[Comparing 3rd Downs Only to All Downs](#Comparing-3rd-Downs-Only-to-All-Down)

[About Tracking Data](#About-Tracking-Data)

- [Comparing KNN Models With/Without Tracking](#Comparing-KNN-Models-With/Without-Tracking)
 
[Future Exploration](#Future-Exploration)

> ## The Data

[https://www.kaggle.com/competitions/nfl-big-data-bowl-2024/data](https://www.kaggle.com/competitions/nfl-big-data-bowl-2024/data)
	
 Historical data for the first 9 weeks of NFL 2023 season included the following data sets:<br>
		games.csv, plays.csv, players.csv, tracking.csv, and tackles.csv

<img src="images/data-access-commands-kaggle.jpg" width="600"/>

[https://site.api.espn.com/apis/site/v2/sports/football/nfl/teams](https://site.api.espn.com/apis/site/v2/sports/football/nfl/teams)<br>
	Used for visualization

<img src="images/data-access-commands-espn.jpg" width="600"/>

> ## QuickDBD

This ID was needed to identify individual plays across the entire database:

- **play_uuid** - a unique Play ID built from gamesID and playsID

![quickdbd image](images/QuickDBD-export.png)

> ## Features

### Features used from source

- **gameId:** Game identifier, unique (numeric)
- **playId:** Play identifier, not unique across games (numeric)
- **ballCarrierId:** The nflId of the ball carrier (receiver of the handoff, receiver of pass or the QB scrambling) on the play (numeric)
- **playDescription:** Description of play (text)
- **quarter:** Game quarter (numeric)
- **down:** Down (numeric)
- **yardsToGo:** Distance needed for a first down (numeric)
- **possessionTeam:** Team abbr of team on offense with possession of ball (text)
- **defensiveTeam:** Team abbr of team on defense (text)
- **gameClock:** Time on clock of play (MM:SS)
- **preSnapHomeScore:** Home score prior to the play (numeric)
- **preSnapVisitorScore:** Visiting team score prior to the play (numeric)
- **playResult:** Net yards gained by the offense, including penalty yardage (numeric)
- **absoluteYardlineNumber:** Distance from end zone for possession team (numeric)
- **offenseFormation:** Formation used by possession team (text)
- **defendersInTheBox:** Number of defenders in close proximity to line-of-scrimmage (numeric)
- **preSnapHomeTeamWinProbability:** The win probability of the home team before the play (numeric)
- **preSnapVisitorTeamWinProbability:** The win probability of the visiting team before the play (numeric)
- **homeTeamWinProbabilityAdded:** Win probability delta for home team (numeric)
- **visitorTeamWinProbabilityAdded:** Win probability delta for visitor team (numeric)

### Newly Created Features

These features were created from the existing historical play data:

- **converted** - this equals 1 when playResult equals or exceeds yardsToGo, otherwise 0
- **week** - numeric (1-9) week of the season

Deliberate language within the playDescription column indicates:

- **playType** - pass/run
- **ballDirection** - right/left/middle/none

### Cumulative Averages - described

The following generated features represent historical, cumulative successes/failures. 
The concept is to capture trends in the data over time.

**cumulativeOverall_O** - offensive successful conversions; cumulative average prior to the snap<br>
**cumulativeOverall_D** - defensive successful blocks; cumulative average prior to the snap

**cumulativePerFormation_O** - offensive successful conversions with each O-formation; cumulative average prior to the snap<br>
**cumulativePerFormation_D** - defensive successful blocks against each O-formation; cumulative average prior to the snap<br>

**cumulativePerBoxCt_O** - offensive successful conversions against each D-box count; cumulative average prior to the snap<br>
**cumulativePerBoxCt_D** - defensive successful blocks with each D-Box count; cumulative average prior to the snap<br>

**carrierSuccessOverall** - ball carrier successful conversions; cumulative average prior to the snap<br>
**carrierSuccessPerFormation** - ball carrier successful conversions with each O-formation; cumulative average prior to the snap<br>
**carrierSuccessPerBoxCt** - ball carrier successful conversions against each D-box count; cumulative average prior to the snap<br>

### Cumulative Averages - example

The following shows the running success rate - before the ball is snapped - in the first 5 plays of the season, where Buffalo was the possession team facing 5 defenders in the box.

![cumulative example image](images/cumulative_example.png)

> ## MatPlotLib Visualization - the field and positions

This is the player and ball positions of a play just prior to the snap in week 3 of the season. Cleveland is lined up in a singleback offensive formation against Pittsburgh's 7 defenders in the box. There are two yards to go for a first down. The play is a run to the left, which only results in a gain of 1 yard and thus a failed first down conversion.

![matplot image](images/matplot-field.jpg)

> ## Correlations

The following image is a heatmap generated by the Seaborn correlation tool, showing the degree of relationships of potential features. 

<img src="images/corr_heatmap.png" width="800"/>

This is a list, in order of absolute strength, of correlations of potential features to the binary result of 'conversion':

<img src="images/corr_abs_list.png" width="300"/>

> ## The Training

> ## Random Forest - Feature Importance

> ## KNN

> ## Deep Model - Keras/TensorFlow

> ## Increasing the Volume of Data Over 9 Weeks

> ## Comparing 3rd Downs Only to All Down

> ## About Tracking Data

> ## Comparing KNN Models With/Without Tracking

> ## Future Exploration
