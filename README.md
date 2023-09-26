<p align="center">
  <img width="400" height="300" src="https://github.com/yash-pimpale/T20_World_Cup_2022_Dream_Team_Selection/blob/main/Media/T20I_WC_logo.jpg">
</p>

# T20 World Cup 2022 Dream Team Selection

## Overview

The objective of this project is to carefully choose a top-performing team of 12 players for the ICC T20 World Cup 2022. This selection process will take into account each player's performance, as well as their specific roles, during both the qualifiers and the super 12 stage of the tournament. 

The Team formed must statisy below criteria:-

1. The team should be able to score at least 180 runs on an average
2. They should be able to defend 150 runs on an average

## Data Sources

- ESPN ICC Men's T20 World Cup, 2022/23 : [ESPN](https://www.espncricinfo.com/records/tournament/icc-men-s-t20-world-cup-2022-23-14450)

Below mentioned data files are used in this project:- 

- Batting Summary : This file provides a comprehensive overview of each player's batting performance. It includes crucial details like the opponent team, runs scored, balls faced, fours hit, sixes hit, and the player's strike rate, etc.
- Bowling Summary : This file contains valuable information regarding each player's bowling performance. It includes data such as the opponent team, overs bowled, runs conceded, wickets taken, dot balls bowled, and the number of fours and sixes conceded, etc.
- Match Summary : It includes essential match-related information, such as the participating teams (Team 1 and Team 2), the match's winner, the margin of victory or defeat, the location or ground where the match took place, and the date of the match.
- Players : It contains vital player-specific details, including the player's team, batting style, bowling style, role in the team, and a brief description, etc.

Note : It's important to note that the data encompasses matches played in both the Qualifier and Super 12 stages of the tournament.

## Requirement Scoping

To facilitate the team formation process, we will categorize players into five distinct roles, each with its specific set of criteria. This role-based approach simplifies the team selection process, ensuring that players are chosen based on their suitability for specific playing styles.

Below criteria are designed to identify and select players for specific role:-

### 1. Openers:
  - Batting Average should be greater than 30
  - Batting Strike Rate should be greater than 140
  - Total Innings Batted should be greater than 3
  - Boundary percentage Faced should be greater than 50
  - Batting position should be less than 4

### 2. Anchors:
  - Batting Average should be greater than 40
  - Batting Strike Rate should be greater than 125
  - Total Innings Batted should be greater than 3
  - Average Balls Faced should be greater than 20
  - Batting position should be greater than 2

### 3. Finishers:
  - Batting Average should be greater than 25
  - Batting Strike Rate should be greater than 130
  - Total Innings Batted should be greater than 3
  - Average Balls Faced should be greater than 12
  - Batting position should be greater than 4
  - Total Innings Bowled should be greater than 1

### 4. All rounders:
  - Batting average should be greater than 15
  - Batting Strike Rate should be greater than 140
  - Total Innings Batted should be greater than 2
  - Batting position should be greater than 4
  - Total Innings Bowled should be greater than 2
  - Bowling Economy should be less than 7
  - Bowling Strike Rate should be less than 20

### 5. Fast Bowlers:
  - Total Innings Bowled should be greater than 4
  - Bowling Economy should be less than 7
  - Bowling Strike Rate should be less than 16
  - Bowling Average should be less than 20
  - Dot Ball percentage should be greater than 40

## Implementation

Based on above mentioned details we will now implement the project in Microsoft Power BI.

### 1. Data Loading and Preprocessing

We'll start by importing data from CSV files into Power BI tables and then perform various data transformation tasks, including renaming columns, converting values, and creating calculated columns.

- Column Renaming: To make the data more user-friendly, we will rename certain columns. For example, columns with abbreviated names such as 0's, 4's, etc will be given clearer titles.

- Data Transformation: We will convert strings column e.g. "out" to number data types and update values 0 (out) or 1(not out) accordingly.

- Calculated Columns: We will create new columns that calculate important metrics for our analysis. For example, we calculate "Boundary Runs" by summing the number of fours and sixes a player hits. Also, we determine the "Stage" of the match basis match date, indicating whether it was a Qualifier or Super 12 stage match.

Below is the preview of the data:-

<p align="center">
  <img width="700" height="400" src="https://github.com/yash-pimpale/T20_World_Cup_2022_Dream_Team_Selection/blob/main/Media/Batting_Summary_Table.png">
</p>

### 2. Creating Key Parameters

We will now create key parameters which are essential for performing calculations and analysis. These parameters allow us to define custom calculations/aggregations based on existing column data. For e.g. 
- Total Runs : It is calculated as the sum of runs scored by players in the batting summary table i.e. SUM(batting_summary[runs]).
- Batting Average : It represents the average number of runs scored per innings played. Calculated using the formula - DIVIDE([Total Runs],[Total Innings Dismissed],0).

List of all key parameters created and used in this project is [here](https://github.com/yash-pimpale/T20_World_Cup_2022_Dream_Team_Selection/tree/main/).

<p align="center">
  <img width="700" height="400" src="https://github.com/yash-pimpale/T20_World_Cup_2022_Dream_Team_Selection/blob/main/Media/Key_Parameters.png">
</p>

### 3. Data Modeling

We will now establish relationships between the tables. This step is crucial for integrating data from different sources and tables, enabling us to create meaningful visualizations and perform analyses across related data.

- Identify Key Fields: We first identify the key fields in each table that can be used to connect the tables. These key fields should have unique identifiers, such as Match_id and Name, that are common across multiple tables. 

- Create Relationships: Using Power BI's modeling, we will create relationships between the tables based on these fields.
  1. We establish a many-to-one relationship between the "Batting Summary" and "Players" table and the "Bowling Summary" and "Players" tables using the "Name" field.
  2. We also create a many-to-one relationship between the "Batting Summary" and "Match Summary" table and the "Bowling Summary" and "Match Summary" tables using the "mattch_id" field.
 
<p align="center">
  <img width="700" height="400" src="https://github.com/yash-pimpale/T20_World_Cup_2022_Dream_Team_Selection/blob/main/Media/Data_Modelling.png">
</p>

### 4. Creating Interactive Reports

Create interactive report for each type of role by adding respective filters as mentioned above. Add slicer for qualifier and super 12 stage. Create buttons for each role so that user can navigate to respective page by click on it (control + click). Add table displaying selected players based on criteria and add tooltip on player name to display indetailed details of the player. Add onclick functionality such that when user clicks on the player, its statistics are displayed (otherwise hidden). Select multiple player to check their combined stats. Add 4 separate stacked line chart for performance metrics. 

Create interactive reports in Power BI involves designing visualizations and user-friendly features to help users analyze data effectively. Here's how we can create interactive reports for each type of role and incorporate the specified features:

- Role-Specific Pages: We will create separate report pages for each role i.e. Openers, Anchors, Finishers, All Rounders and Fast Bowlers. Added filters specific to each role, allowing users to select a role of interest. These will help users focus on the desired player criteria for each role.

- Stage Slicers: Included slicer that allow users to filter data based on the qualifier and Super 12 stages, enabling them to compare player performance in different tournament stages.

<p align="center">
  <img width="700" height="400" src="https://github.com/yash-pimpale/T20_World_Cup_2022_Dream_Team_Selection/blob/main/Media/Pages_and_Slicer.png">
</p>

- Role Buttons: Created buttons for each role to enable users to navigate to the respective role page with a simple click (Ctrl + click).

- Player Selection Table: Added a table to display selected players who meet the role-specific criteria. This table includes player names, role-specific key statistics and an interactive tooltip. When users hover over a player's name, the tooltip will display detailed player information, such as player's picture, country, batting and bowling statistics (depending upon the role). Also allowed users to select multiple players from the table to compare their combined statistics.

<p align="center">
  <img width="700" height="400" src="https://github.com/yash-pimpale/T20_World_Cup_2022_Dream_Team_Selection/blob/main/Media/Report_Hover_Functionality.png">
</p>

- OnClick Functionality: Incorporated onClick functionality for player names in the selection table. When a user clicks on a player's name, additional key statistics such as Batting Average, Strike Rate, Economy, etc will become visible (otherwise hidden) for that player according to the role.

<p align="center">
  <img width="700" height="400" src="https://github.com/yash-pimpale/T20_World_Cup_2022_Dream_Team_Selection/blob/main/Media/Report_OnClick_Functionality.png">
</p>

- Stacked Line Charts: Created four separate stacked line charts to visualize performance metrics. These charts can include metrics like batting average, strike rate, wickets taken, or any other relevant statistics vs match day, for players in each role.

Below video showcases all the functionalities and capabilities of this Power BI report. It serves as a comprehensive demonstration of how users can interact with and leverage the report for informed decision-making.

<p align="center">
  <img width="700" height="400" src="https://github.com/yash-pimpale/T20_World_Cup_2022_Dream_Team_Selection/blob/main/Media/World_Cup_Dream_Team_Report.gif">
</p>

Note: File name is changed post this video was captured.

## Conclusion

This project demonstrates the power of data analysis and visualization in sports selection process. It enables cricket enthusiasts, coaches, and team management to make informed decisions and assemble the most competitive team for a prestigious tournament like the ICC T20 World Cup. The project's structured approach and user-friendly reports empower stakeholders to optimize player selection based on specific criteria and roles, ultimately enhancing the team's chances of success.
