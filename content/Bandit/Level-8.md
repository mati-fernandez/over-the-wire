#### Concept
Filtering unique lines by pre-sorting data.
#### Key Commands
`sort data.txt | uniq -u`
#### Walkthrough
The `data.txt` file contains thousands of lines, and the password is the only line that occurs exactly once. Since the `uniq` command only compares **adjacent** lines, we must first use `sort` to group identical lines together. Then, we pipe the output to `uniq -u` to discard all duplicates and display only the unique entry.
#### Key Takeaways
- **`sort`**: An indispensable prerequisite before using `uniq`.
- **`uniq -u`**: Returns only lines that have no copies (truly unique).
- **`uniq -c`**: (Extra Tip) A useful flag to count the occurrences of each line, often used in log analysis to find the most frequent events.
#### Pass 9
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM