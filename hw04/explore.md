## Task 3 Exploration:
To check how big the dataset is, we can use wc -l clean_dialog.csv to check number of lines and find:
>> 36860 clean_dialog.csv
To check what the structure of the data is, we can pull the column values with "head -n 1 clean_dialog.csv"
>> "title", "writer", "pony", "dialog"
To check how many unique episodes, we need a few piped commands. Awk to filter, sort to find unique, and wc to count.
Specifically "awk -F, 'NR>1 {print $1}' clean_dialog.csv | sort -u | wc -l"
awk -F with NR>1 ignores row 1, {print $1} outputs only first comma sep value.
Sort -u sorts all alphabetically and only keeps unique entries with -u flag.
Wc -l returns line count of the file of all episode titles, giving 196 lines.
When testing with awk, we can see that one notable difficulty is the number of commas present in the script speechtext. These will potentially disrupt the way we read a csv file, as some lines have as many as 10 commas in the script.
Otherwise, theres a lot of name repitition across the script and title fields as well that could make this difficult.


## Task 4 Speaker Freq:
At first I tried commands like grep "Twilight" clean_dialog.csv | wc -l, which tenatively worked, but Twilight was more than double the other entries so I imagined some script or titles included character names.
When changing to awk -F, 'NR>1 {print $3}' clean_dialog.csv | grep "Twilight" | wc -l, results were much more reasonable, with Twilight still being a clear winner.
Finally, I used awk -F, 'NR>1' clean_dialog.csv | wc -l to get the total lines and used all command results to calculate percentages in a python file.
