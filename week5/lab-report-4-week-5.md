# Week 5 Lab Report

### The command I will be researching is grep

## grep -c 
--> gives the count of the matching strings found in a file

### Example 1
```
[ashaikh@ieng6-201]:biomed:132$ grep -c "BMI"  1468-6708-3-1.txt
32
```
* There are 32 instances of "BMI" in the file.
* This is useful because instead of printing out the lines containting this word, it prints out the _number_ of lines instead. So to get this number without using -c, we would first have to use grep and print the results to a file, then use wc to count the number of lines. -c makes less work.

### Example 2
```
[ashaikh@ieng6-202]:~:134$ cd docsearch/technical/plos
[ashaikh@ieng6-202]:plos:135$ grep -c "lifespan" journal.pbio.0020012.txt                                      
19
```
* There are 19 instances of the string "lifespan" in the file journal.pbio.0020012.txt
* In a file that records results of some sort, it may be useful to see how many times certain values appeared, especially if you wanted to graph them. grep -c makes it easy to count the number of times.

### Example 3
```
[ashaikh@ieng6-202]:plos:136$ grep -c "Darwin"  journal.pbio.0020439.txt
2
```
* grep -c shows that there are two instances of "Darwin" in the file.
* In this case, it could be useful to see how many times Darwin's work was cited in the text file.


## grep -A n -B m
--> Prints n number of lines after the line with the matching string, and m number of lines before the line with the matching string
     
--> You can also use it with either A or B

### Example 1
```
[ashaikh@ieng6-202]:~:138$ grep -A 2 -B 1 "year 2000" docsearch/technical/government/Gen_Account_Office/d0269g.txt

complex organization in the world-expended approximately $1.8
trillion dollars in fiscal year 2000. As the steward of taxpayer
dollars, it is accountable for how its agencies and grantees spend
those funds, and is responsible for safeguarding against improper
--
Comptroller and Auditor General has qualified his opinion on DWP's
fiscal year 1995 through fiscal year 2000 financial statements
because of the level of fraud and error identified in the benefit
programs. This served to reinforce the message that high levels of
--
an annual estimate of improper payments in the Medicare
Fee-for-Service program in 1996. In fiscal year 2000, it reported
estimated improper Medicare Fee-for-Service payments of $11.9
billion, or about 7 percent of such benefits. HHS' reporting and

```
* This code looked for lines in the file d0269g.txt containing the string "year 2000", and printed it as well as the next two lines and previous one line.
* This could be useful if you want to reference a certain topic in a text file. All you have to do is look up a keyword and you will get the lines around it, which can help you to quickly find what was said about that keyword. So in this instance a snapshot of what happened in the "year 2000" in this file is printed.

### Example 2
```
[ashaikh@ieng6-202]:~:138$ grep -A 1 "higher risk" docsearch/technical/biomed/1468-6708-3-3.txt
recent trials have suggested that higher risk patients with non-ST elevation acute coronary syndromes fair better when
```
* This code searched for the string "higher risk" in the file 1468-6708-3-3.txt, and then printed out the line it was found on as well as the line after it.
* If a quote was needed from this text, you can find it easily with this command and copy and paste the relevant information.

### Example 3
```
[ashaikh@ieng6-202]:~:142$ grep -B 2 "9:12" docsearch/technical/911report/chapter-1.txt
    At 9:00, American Airlines Executive Vice President Gerard Arpey learned that communications had been lost with American 77. This was now the second American aircraft in trouble. He ordered all American Airlines flights in the Northeast that had not taken off to remain on the ground. Shortly before 9:10, suspecting that American 77 had been hijacked, American headquarters concluded that the second aircraft to hit the World Trade Center might have been Flight 77. After learning that United Airlines was missing a plane, American Airlines headquarters extended the ground stop nationwide.

    At 9:12, Renee May called her mother, Nancy May, in Las Vegas. She said her flight was being hijacked by six individuals who had moved them to the rear of the plane. She asked her mother to alert American Airlines. Nancy May and her husband promptly did so.
```
* This code searched for the string "9:12" and printed the line it was on, as well as the two lines before it.
* In this example, the text file contains times that certain events happened. So it is useful because you can find out what happened at "9:12" and just before it.

## grep -e 
--> allows you to look for multiple strings in a file
### Example 1
```
[ashaikh@ieng6-202]:biomed:148$ grep -e "apoptosis" -e "die" -e "death" 1471-213X-1-11.txt

        mesenchymal cells on the cell cycle and death
        studies [ 1, 2, 9, 10], and those of others [ 3, 4, 5, 6,
        growth and die at a relatively rapid rate. Alternatively,
        suicidal state (apoptosis) by mesenchymal cells in a given
        The terminal stage of cell differentiation is apoptosis,
        during which cells undergo DNA fragmentation and die.
        apoptosis of epithelial cells.
```
* The code looks for all three strings in the provided file, and prints out the lines they were found on. It doesn't search for the strings one at a time, but rather all at once, because the lines which contain "death", "die" and "apoptosis" are not output in order.
* This could be useful if you are looking for mentions of a specific thing which is referenced by many names in a file, and don't want to repeatedly write grep commands.


### Example 2
```
[ashaikh@ieng6-202]:docsearch:144$ grep -e "Bayoumi" -e "Baioumi" technical/911report/chapter-7.txt

                somewhat suspect. (He likewise denied knowing Omar al Bayoumi-a man from San Diego
                Bayoumi and Caysan Bin Don at a halal food restaurant on Venice Boulevard in Culver
                City, a few blocks away from the King Fahd mosque. Bayoumi and Bin Don have both
                told us that they had driven up from San Diego earlier that day so that Bayoumi
                could address a visa issue and collect some papers from the Saudi consulate. Bayoumi
                on Bayoumi to translate for him.
                were having a hard time, especially because they did not know anyone. Bayoumi told
        
```
* This looks for lines which contain "Bayoumi" or "Baioumi", and prints the lines which match either string.
* This is useful if you are looking for something that you are unsure about the spelling of.

### Example 3
```
[ashaikh@ieng6-202]:biomed:147$ grep -e "center" -e "centre" 1468-6708-3-4.txt

          A multicenter, randomized, double-blind, three
          A multicenter, randomized, open-label, parallel-design
          A multicenter, randomized, double-blind,
```
* grep -e looks for the strings "center" and "centre", and then outputs the lines they was found on.
* In this case, it could be useful to check for alternate spellings, and also, if you are prone to making typos on the word "center", it could be useful to check for typos.