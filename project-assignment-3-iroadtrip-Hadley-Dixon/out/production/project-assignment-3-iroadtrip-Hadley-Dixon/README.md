# CS 245 (Fall 2023) - Assignment 3 - IRoadTrip

Can you plan the path for a road trip from one country to another?

Change the java source code, but do not change the data files. See Canvas for assignment details.

## My Implementation
According to responses from Prof. Brizan and Prof. Veomett on Slack, as well as the project description, I have implemented Project 3 in the following way:

- I first read in 'state_name.tsv'. This was because we should only include countries that exist in 2020. I extracted the 3-letter unique ID's from each country in 'state_name.tsv' with data from in 2020.
  - I created a Hashmap of these unique IDs with the associated country name as their key. (Note that these keys will later change to reflect 'official' spelling).

- I then chose one standard official spelling. The official spelling is the spelling from 'borders.txt'. 
  - I created a transform method to convert un-official country names. I transformed the original country keys in country name map (in 'state_name'.tsv), so that they aligned with the 'official' country name in 'borders.txt'.

- Next, I created an adjacent country graph, reading in 'borders.txt', and setting a default distance between capitals to be 0. For a country to be added, it must meet 2 requirements .
  - (1) The country existed in my country name map, meaning that it had a 3-letter ID from 2020 (disregarding countries who did not have 2020 data).
  - (3) The country was not already in the graph.

- Lastly, I read in 'capdist.csv', using the 3-letter IDs in my country name map to extract distances between capitals (the weights).

- The previous steps allowed me to address the following potential issues
  - 'capdist.csv' contains country codes that don’t exist in the 'state_name.tsv'.
  - 'border.txt' contains country names that are not associated with a 2020 3-letter ID in 'state_name.tsv'.
  - Countries present in both 'state_name.tsv' and 'borders.txt' are sometimes referred to by different spellings.
- I was able to find the intersection of countries that (1) have a unique ID (2) have an official spelling (3) have distance data present
  - When a country meets this intersection, it was added to my country graph.
  - This means that there is a chance that the user inputs a real country, but it is not a valid country in my graph, due to it not falling in this intersection
    - There is an output that lets the user know this, and refers them to this README.md

- This implementation proved useful in eliminating null countries (countries without an ID, without distance data, or who ceased to exist in modern day) while also still adding countries with no adjacent countries/islands.
  - There were a few outliers however, which are as follows:
    - (1) South Sudan: has a 3-letter ID from 2020, has adjacent countries in 'borders.txt', *but* has no distance data.
    - (2) Kosovo: has a 3-letter ID from 2020, has adjacent countries in 'borders.txt', *but* has no distance data.
  - To address this, there a few lines of hardcore to prevent crashing, which ideally I would have likely to circumvent, however this was not feasible under time constraints.

## Sources used
(1) Graph structure: https://www.geeksforgeeks.org/implementing-generic-graph-in-java/

(2) Scanner on .txt: https://www.geeksforgeeks.org/different-ways-reading-text-file-java/

(3) Exceptions: https://www.tutorialspoint.com/javaexamples/exception_method.htm

(4) Scanner on .csv: https://www.youtube.com/watch?v=rj6vyIn90zk

(5) Scanner .tsv: https://codepal.ai/code-generator/query/0pkdvNiV/java-program-read-student-information

(6) Scanner for user input: https://www.theserverside.com/tutorial/Your-top-Java-user-input-strategies

(7) Dijkstra's Algorithm: https://www.freecodecamp.org/news/dijkstras-algorithm-explained-with-a-pseudocode-example/

(8) Lecture slides