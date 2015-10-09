# NetApp

Brian McKean from NetApp presented to the class a data analysis problem he'd
like to get some help on.

# Overview

Listen to his presentation carefully. Write down the answers to the following
questions to show your team's understanding of the basics of the problem.

## What is the problem? 
Can lower-endurance SSDs be used in NetApps products without increasing rates of drive wear-out?

## Why is the problem important? 
If lower-endurance SSDs continue to meet consumer needs without increasing rates of SSD wear-out, the cost of manufacturing products would be significantly reduced.

## What dataset has been made available?
The ASUP file, which contains information on how many writes are made over a certain period of time. 

## What specific questions are being raised?
How many ASUPs can be used to accurately analyze DWPD?

# Q/A session

We will run a Q/A session. Before the session, compile a list of questions you
want to ask. Then, teams will take turn to ask Brian follow up questions.
Each team gets to ask one question each time. Write down the questions your team
wanted to ask and the answers you received. If another team happens to ask the
same question, simply write down the answer you heard.

## Are Observation/Base Times timestamps that correspond to the date in the Date column?
Yes; the Observation Time corresponds to the Date.

## In theory (in a perfect world), should each system have an entry for every day?
Yes, but not all systems are reporting their data correctly.


# Approach

Based on the information you've obtained during the Q/A session, come up with
plan how your team will tackle this problem.

## How should the dataset be imported into Tableau?
Import the csv into tableau.

## How should the work be distributed among the team members?
Initially each team member should individually explore the data & report back to the team any interesting findings. Then as a team we will refine our question and create a strategy to to visualize the data. 

## What types of charts or visualizations to use to support the answer?
The appropriate visualization depends on exactly what is being visualized; this dataset contains both discrete and continuous variables, so in some cases, scatter plots may be appropriate (continuous vs. continuous) data, whereas in other cases, bar graphs may be appropriate (discrete vs. continuous).

## What questions may be too complex for Tableau and may require custom scripts to be written?
In some cases, it would be nice to compute additional statistics using the data provided. For example, if a particular system exhibits the non-incrementing basetime bug, it would be nice to be able to compute adjusted basetimes off of the existing data, which may be more representative of the actual reporting behavior of the system. 