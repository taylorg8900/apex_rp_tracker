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
	- the goal here is to, in the future, generate graphs from the data to make it more visible *exactly* how quickly you are gaining or losing RP

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

Anyway, if I do any of that it will have to be another program. This one is just 
about appending values to a .csv file.

# Requirements analysis

I am going to be using Python for this program, because it is a very simple
program and I can't be bothered to learn how to use anything else for this project. 

libraries
- We will need sys.argv since this program takes arguments. 
- Time library, since we need to know when the program gets ran.

# Design

Here are some of the things that the program needs to be able to do:
- appending the .csv file
  - if the file does not already exist, then create one with a certain name (maybe rp.csv?).
  - if the file does exist, then append the argument given to it
  - add time values to the file 
  - Decide between adding raw RP values, or how much to be added to the previous value?
    - I could examine sys.argv for an argument such as 'add', and if that exists, then add the following value to what is stored in the last row of the csv file. if 'add' is not present, then the user is trying to append a raw RP value.

Here are some things the program does not need to know how to do:
- editing values in the csv file. The reason for this is that if someone wants to change something, they can just edit it in notepad or something. its not really useful to have that functionality here

How do we decide how to store the date/time information?
- I would like to store the raw timestamp (time in milliseconds) first of all, to be potentially used in the future. No reason not to store that information
- We can store the year/month/day/hour/minute/second as separate fields in the .csv file
- We can try to convert that information to a 'datetime' or ISO 8601 format, to be automatically detected in a spreadsheet and used in graphs.
  - the format for this is \[YYYY-MM-DD HH:MM:SS]
  - this might not work immediately since having this format means it can't be a string. I'll cross that bridge when I get to it.

some examples of usage for the program that i am imagining...
```commandline
rp.py help

About: This program takes an RP value, and appends it to a .csv file called 'rp.csv' along with the date and time in which it is entered.
       Use the 'add' argument to append an amount of RP, added to the previous entry in the csv file.
       Use the 'rm' argument to append an amount of RP, subtracted from the previous entry in the csv file.
       Don't use either argument to simply append an RP value to the file.

Usage: [ add | rm ] VALUE
```

```commandline
rp.py 3004
append '3004' to csv file? y/n: 
```
```commandline
rp.py add 36
(3010 + 36 = 3046)
append '3046' to csv file?  y/n: 
```
```commandline
rp.py rm 36
(3010 - 36 = 2974)
append '2974' to csv file? y/n: 
```
I think having a function to see about whether or not 'rp.csv' exists will be good for more than just creating the file. It will also 
mean that the program will catch if the user changes the name of the .csv file to something else, and won't explode since it can 
just create a brand new file and keep chugging along.

Here are all of the functions I think I will need:
- message functions
  - print out about/usage message
  - print out the add/subtract calculation line
  - print the 'append...?' line
- csv file functions
  - find the value in the last record of the csv file
  - check if the file exists in the same directory as the program
  - append the rp and date/time fields to the csv file
- time functions
  - raw milliseconds / timestamp
  - formatted with ISO 8601 format / YYYY-MM-DD HH:MM:SS 
  - find the year, month, day, hour, month, second