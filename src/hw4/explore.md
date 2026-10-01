# Task 3

```
ls -lth
wc -l clean_dialog.csv
``` 
The dataset is 4.7MB and has 36860 lines


```
head -n 1 clean_dialog.csv
```
There are 4 columns. The title is the name of the episode, the writer is the person credited for that episode, dialog contains all the lines, and pony refers to the character speaking that line.

```
csvtool namedcol title clean_dialog.csv | tail -n +2 | sort -u | wc -l
```
There are 197 episodes in the dataset

```
csvtool namedcol dialog clean_dialog.csv | grep '\['
```
The dialogue text includes braketed reactions such as [gasp] or [sighs]


# Task 4
```
TOTAL=$(tail -n +2 clean_dialog.csv | wc -l)
echo "pony_name,total_line_count,percent_all_lines" > line_percentages.csv

for name in "Twilight Sparkle" "Rarity" "Pinkie Pie" "Rainbow Dash" "Fluttershy"; do
    count=$(csvtool namedcol pony clean_dialog.csv | tail -n +2 | grep -c "^${name}\$")
    percent=$(python3 -c "print(round(100*$count/$TOTAL, 3))")
    echo "\"$name\",$count,$percent" >> line_percentages.csv
done
```
