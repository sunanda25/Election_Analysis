# Election_Analysis

## Project Overview
A Colorado Board of Elections employee has given you the following tasks to complete the election audit of a recent local congressional election.

1. Calculate the total number of votes cast.
2. Get a complete list of candidates who received votes.
3. Calculate the total number of votes each candidate received.
4. Calculate the Percentage of votes each candidate won.
5. Determine the winner of the election based on popular vote.

## Resources
- Data Source: election_results.csv
- Software: Python 3.7.6, Visual Studio Code

## Summary
The analysis of the election show that:
- There were 369,711 votes cast in the election.
- The candidates were:
  - Charles Casper Stockham
  - Diana DeGette
  - Raymon Anthony Doane
- The candidate results were:
  - Candidate Charles Casper Stockham received "23.0%" of the vote and "85,213" number of votes.
  - Candidate Diana DeGette received "73.8%" of the vote and "272,892" number of votes.
  - Candidate Raymon Anthony Doane received "3.1%" of the vote and "11,606" number of votes.
- The winner of the election was:
  - Candidate Diana DeGette, who received "73.8%" of the vote and "272,892" number of votes.

## Overview of Election Audit
A Colorado Board of Elections employee, Tom wants to audit the recent local congressional election using Python. The audit should include the below findings:
- Total number of votes cast
- Total number of votes and percentage of votes for each candidate
- Winner of the election based on popular vote

Using Visual Studio Code editor, the above findings are calculated, and the results are shown in the summary above. After looking at the results Tom wants to find the below:
- Number of votes and percentage of votes for each county
- The county with the largest turnout

## Election Audit Results
1. Total votes cast in the congressional election are calculated by counting the number of rows in the CSV file.
~~~
# Read the csv and convert it into a list of dictionaries
with open(file_to_load) as election_data:
    reader = csv.reader(election_data)

    # Read the header
    header = next(reader)

    # For each row in the CSV file.
    for row in reader:

        # Add to the total vote count
        total_votes = total_votes + 1
~~~

![image](https://user-images.githubusercontent.com/76491891/110859867-17b88b00-828a-11eb-867a-a329bc34b11f.png)

2. Number of votes and the percentage of votes for each county are calculated by using an IF statement and maintaining a list of distinct counties.

~~~
# Write an if statement that checks that the
        # county does not match any existing county in the county list.
        if county_name not in county_options:

            # Add the existing county to the list of counties.
            county_options.append(county_name)

            # Begin tracking the county's vote count.
            county_votes[county_name] = 0

        # Add a vote to that county's vote count.
        county_votes[county_name] += 1      
~~~

![image](https://user-images.githubusercontent.com/76491891/110859812-ff487080-8289-11eb-8662-9b595c83d827.png)

3. County with the largest turnout is calculated using a FOR loop to scan each county and an IF loop to keep track of the county with the most number of votes.

~~~
# Write a for loop to get the county from the county dictionary.
    for county_name in county_votes:
        
        # Retrieve the county vote count.
        votes = county_votes[county_name]
        
        # Calculate the percentage of votes for the county.
        vote_percentage = float(votes) /float(total_votes) * 100

        # Print the county results to the terminal.
        county_results = (f"{county_name}: {vote_percentage:.1f}% ({votes:,})\n")
        print(county_results)
        
        # Save the county votes to a text file.
        txt_file.write(county_results)
        
        # Write an if statement to determine the winning county and get its vote count.
        if (votes > largest_county_count):
            largest_county = county_name
            largest_county_count = votes
~~~

![image](https://user-images.githubusercontent.com/76491891/110859989-3ae33a80-828a-11eb-8aef-c97da415bba9.png)

4. Each candidate's votes and percentage of votes are calculated using an IF statement and maintaining the values with the help of a dictionary.
~~~
# If the candidate does not match any existing candidate add it to
        # the candidate list
        if candidate_name not in candidate_options:

            # Add the candidate name to the candidate list.
            candidate_options.append(candidate_name)

            # And begin tracking that candidate's voter count.
            candidate_votes[candidate_name] = 0

        # Add a vote to that candidate's count
        candidate_votes[candidate_name] += 1
~~~

![image](https://user-images.githubusercontent.com/76491891/110860110-5d755380-828a-11eb-80cb-5b025ebb08ba.png)

5. The vote count and percentage of total votes for the winning candidate are calculated by comparing each candidate's vote count and vote percentage with the previous candidate.
~~~
# Determine winning vote count, winning percentage, and candidate.
        if (votes > winning_count) and (vote_percentage > winning_percentage):
            winning_count = votes
            winning_candidate = candidate_name
            winning_percentage = vote_percentage
~~~

![image](https://user-images.githubusercontent.com/76491891/110860147-6a924280-828a-11eb-9495-4547adfde502.png)

## Election Audit Summary
Below are a couple of examples to modify the script and make it usable for any election:
- The script can be modified to take input from the user regarding the type of election (State, Federal, etc.). By using the input provided by the user, the results can be modified to show data based on the type of election.
- The political party alliance for the candidate is not shown with the current script. By modifying code to display the political party alliance for the candidate it will be more useful for State and Federal elections.
