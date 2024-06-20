## Background
Béatrice Frison once took a bicycle from Grenoble to Kathmandu. (She talks about the trip briefly, in French, on YouTube.) Fortunately, she planned well and did not encounter too many problems. Create an implementation of a shortest path trip between two countries for her or someone else who chooses another such trip.

## Read and associate the data files.

There are three data files. Each file contains data you will need, but — because of the sources — each file is in a different format and has different data. The files are as follows:

a. borders.txt: This file contains data about country borders from the CIA World Factbook, specifically the “Land boundaries” page — https://www.cia.gov/the-world-factbook/field/land- boundaries/. Each line in the file contains the name of a country, followed by a “=” character and zero, one or more countries and border lengths, with each country separated by a “;” caracter.
- This corresponds to the CIA World Factbook entry shown in Figure 1, indicating that the country of Belize shares land borders with Guatemala and Mexico. The numbers associated with each country (266 for Guatemala) represent the length of the border between these countries.
- Some countries have alias names. For example, the country Turkey appears in the CIA World Factbook (and in the borders.txt file) as both as “Turkey” and as “Turkey (Turkiye)”. Your implementation must handle both names.
- Countries which share no borders with other countries have no entries following the “=” character.

b. capdist.csv: The file capdist.csv comes from Kristian Skrede Gleditsch’s site. This file shows the distances between capital cities of many pairs of countries. This file is in CSV (comma- separated value) format, with fields detailed in Table 1. The presence of distances between capital cities does not indicate that the countries are adjacent to each other.
- One of the entries in this file is as follows: 451,SIE,580,MAG,7292,4546; indicating that one country ID = SIE (Sierra Leone, with number = 451) is approximately 7292 km (4546 miles) from another country ID = MAG (Madagascar, with number = 580). You may notice that the existence of an entry in this file does not indicate that a path between countries. For example, there is no land path between Sierra Leone and Madagascar. Your implementation must use the distance kmdist (distance in kilometers) field for approximate distances between countries.
<img width="580" alt="Screen Shot 2024-01-07 at 2 08 27 PM" src="https://github.com/Hadley-Dixon/Road-Trip/assets/104175462/e78a60e7-1733-47d2-8a66-79903eba1d2e">

c. state_name.tsv:ThisfilecontainsthefieldslistedinTable2.Thisallowsyoutoassociate names from the CIA World Factbook file (borders.txt) to the distance file (capdist.csv). This file may contain multiple entries for the same state / country.
- which together indicates that the country of Haiti came into existence twice — once in 1816 and again in 19341. Your implementation must take information corresponding to 2020-12-31, the most recent data contained in this file.
<img width="596" alt="Screen Shot 2024-01-07 at 2 08 58 PM" src="https://github.com/Hadley-Dixon/Road-Trip/assets/104175462/ea17ae17-fdd4-4d41-a84c-d933fd2bcd4c">

## Implement the required classes and functions.

Your repository contains the skeleton of one source file, IRoadTrip.java, with a number of functions which only return default values. You may use additional classes and files if you choose, but you are required to complete the functions listed below. You may assume that the IRoadTrip class will be called through the main function as follows: java IRoadTrip borders.txt capdist.csv state_name.tsv
<img width="629" alt="Screen Shot 2024-01-07 at 2 09 36 PM" src="https://github.com/Hadley-Dixon/Road-Trip/assets/104175462/fd7ca45c-8f9b-4440-aaf5-ea02aab4364a">
- public IRoadTrip(String [] args): This function is the constructor for the IRoadTrip class. The args parameter contains the names of the files as provided to main — i.e. an array (in order): borders.txt capdist.csv state_name.tsv. The constructor must read the files and prepare to execute the implementation to respond to requests. The implementation must halt on any failure here.
- public int getDistance (String country1, String country2): This function provides the shortest path distance between the capitals of the two countries passed as arguments. If either of the countries does not exist or if the countries do not share a land border, this function must return a value of -1. Examples are as found in Table 3.
- public List<String> findPath (String country1, String country2): This function determines and returns the shortest path between the two countries passed as arguments (starting in the capital of country1, ending in the capital of country1, and going through the capitals of each country along the way). This path must start in country1 and end in country 2. If either of the countries does not exist or if there is no path between the countries, the function returns an empty List2. Each element of the list must be a String representing one step in a longer path in the format: starting_country --> ending_country (DISTANCE_IN_KM.), eg:
Thailand --> Burma (573 km.)
- public void acceptUserInput(): This function allows a user to interact with your implementation on the console. Through this function, your implementation is required to receive and validate the names of two countries from a user. The country names must be validated — i.e. your implementation must not accept invalid names. Once two valid country names have been entered by the user, the implementation must print the path between those countries if such a path exists

## Sample Output
Enter the name of the first country (type EXIT to quit): CS245 Invalid country name. Please enter a valid country name.

Enter the name of the first country (type EXIT to quit): Yemen

Enter the name of the second country (type EXIT to quit): Jordan
- Route from Yemen to Jordan:
- Yemen --> Saudi Arabia (1040 km.)
- Saudi Arabia --> Jordan (1323 km.)

Enter the name of the first country (type EXIT to quit): Paraguay

Enter the name of the second country (type EXIT to quit): Colombia
- Route from Paraguay to Colombia:
- Paraguay --> Bolivia (1480 km.)
- Bolivia --> Peru (1069 km.)
- Peru --> Colombia (1880 km.)

Enter the name of the first country (type EXIT to quit): Gabon

Enter the name of the second country (type EXIT to quit): France
- Route from Gabon to France:
- Gabon --> Cameroon (405 km.)
- Cameroon --> Nigeria (963 km.)
- Nigeria --> Niger (788 km.)
- Niger --> Algeria (2561 km.)
- Algeria --> Morocco (958 km.)
- Morocco --> Spain (822 km.)
- Spain --> France (1012 km.)

Enter the name of the first country (type EXIT to quit): EXIT
