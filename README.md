# Purpose

This program aims to solve an issue I have had in the past: While playing 
apex legends, I sometimes want to keep track of my RP (ranked points) between 
games. The way I would do this was to open up google sheets, or excel, or some 
kind of spreadsheet, and add my RP to cells in the spreadsheet and then 
create a graph and view how much I had climbed/fallen for the entire season. There 
are just a couple things that I thought were pretty annoying about this:
- adding rp was kind of tedious
- there was no way to track *when* i obtained or lost RP
- I had a bunch of graphs in various places, due to keeping big RP tables across seasons in the same file

This program will add RP to a .csv file, and keep track of when that 
information was entered into the .csv file as well. This will have these 
benefits over adding RP manually to an excel spreadsheet:
- adding rp won't take any navigation, clicking, or self-organization of a spreadsheet
- the time that the RP was entered can now be tracked
	- the goal here is to generate graphs from the data to make it more visible *exactly* how quickly you are gaining or losing RP

After having a .csv file with a bunch of information in it, whoever is using 
this program could obviously just import it into excel since it is friendly with 
.csv files, but I would also like to create a custom program that will take in 
a date range and print out a custom graph for the user based on that range. I 
think it would be cool to do it this way so you wouldn't have a ton of different 
graphs laying around for each season. I could even have options for displaying 
graphs of particular seasons, or have the most recent season displayed for the 
user if I created some kind of GUI for the program, before they go in and enter 
new information. This might actually turn out to be a cool little pet project 
if I decide to learn how to make an actual program with a GUI. That way, it could 
be shared with anybody, not just people who would run this on the command line.

# Requirements analysis

I am going to be using Python for this program, because it is a very simple 
program and I can't be bothered to learn how to use anything else for this project. 

### libraries

We will need sys.argv since this program takes arguments. I will also probably 
use the time library, but will need to look up documentation for it to find out 
how to get the local time for a machine. 

