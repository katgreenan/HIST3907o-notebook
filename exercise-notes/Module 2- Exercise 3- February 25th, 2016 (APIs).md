### APIs
- APIs let a program on your computer talk to the computer serving the website you're interested in, such that the website gives you the data that you're looking for. That is, instead of you punching in the search terms, and copying and pasting the results, you get the computer to do it. The results come back to you in a machine readable format - often, JSON.

### The Exercise
- Go to The 'Canadiana Discovery Portal': http://search.canadiana.ca/
- Search "ottawa" with the date range set to 1800 to 1900. Hit enter. You should get 56 249 results. (edit: 56,845 as of late Feb 2016)
	- Note the address bar, should say something like: http://search.canadiana.ca/search?q=ottawa&field=&df=1800&dt=1900 
		- Everything after /search is your query, which is the API!
- Scroll through the results, and you'll see a number before the ?
	- http://search.canadiana.ca/search/2*?*df=1800&dt=1900&q=ottawa&field=
		- These numbers should go up to 5625 (10 results per page, so 56249/10) **(edit: 5685 pages)**
- Go to http://search.canadiana.ca/support/api to see a full list of options
	- you want the bit that looks like this: `&fmt=json`
		- Add that to you query URL 
			- Ooh, snazzy
- Retrieving individual item records
	- key for that is called 'oocihm'
		- Each individual record has one, it can be found under something along the lines of ` ],
         "key" : "oocihm.8_04718",'
         	- Having all of these number would make it rather easy to slot them into commands to retrieve individual items records
	         	- Solution? Write a program

### The Program 
- Found [here](https://ianmilligan.ca/api-example-sh/)
- Study the program carefully. There are a number of useful things happening in there, notably 'curl', 'jq', 'sed', 'awk'. 
	- curl is a program for downloading webpages, 
	- jq for dealing with json, and 
	- sed and awk for searching within and cleaning up text. 

### The Instructions (for Mac)
- Do you have wget installed? *Yes*
- Do you have jq installed? *Yes, but it is v. 1.4, not the current 1.5 and I cannot figure out how to update it without uninstalling the entire program. Should I run into issues, I think this is the first thing I should try in order to fix it*
- Now, download api-ex-mac.sh from the repository and save it to your desktop. 
	- This was a fun time, check out my blog for thoughts on this.
- Open terminal and navigate to the desktop
- Run 'api-ex-mac.sh' (**AFTER EDITING IT**)
	- `sudo chmod 700 api-ex-mac.sh`
		- `./api-ex-mac.sh`
#### Editing 
	- Sulk because Atom keeps crashing and it's the editor you like to use the most
		- Figure out that at some point you'd downloaded a new version of Atom instead of just updating your old one, delete that and update the working version like a normal person
- Original, Line 9: `pages=$(curl 'http://eco.canadiana.ca/search?q=montenegr*&field=&so=score&df=1914&dt=1918&fmt=json' | jq '.pages')'`
	- Insert own search query: `search?q=ottawa&field=&df=1800&dt=1900&fmt=json`
		- Tested to ensure it still links to right page? *Yes*
- Original, Line 20: `for i in $(seq.exe 1 $pages)
do

        curl 'http://eco.canadiana.ca/search/'${i}'?q=montenegr*&field=&so=score&df=1914&dt=1918&fmt=json' | jq '.docs[] | {key}' >> results.txt

done`
	-  Insert own search query: 'http://eco.canadiana.ca/search/'${i}'?q=ottawa&field=&df=1800&dt=1900&fmt=json'
- This should be it for edits

**Saved as: Documents -> *Fourth Year.* HIST 3907O. -> API Exercise Material -> api-ottawa-mac.sh**

###### Running the Program
- Open terminal and navigate to the folder where the script is stored on your machine
- Run 'api-ottawa-mac.sh' 
	- `sudo chmod 700 api-ottawa-mac.sh`
		- `./api-ottawa-mac.sh`

**1st Try**
- Enter Terminal
	- `cd documents`
	- `cd HIST 3907O.`
		- `-bash: cd: HIST: No such file or directory`

- Verdict: **Failed**
	-  *Missed a subdirectory between docs and course folder, edited in missing link in the "saved as" bit above in italics.*

**2nd Try**
- Enter Terminal
	- `cd documents`
	- `cd Fourth Year.`
		- `-bash: cd: Fourth: No such file or directory`
	- `cd FourthYear.`
		`-bash: cd: FourthYear.: No such file or directory`

- Verdict: **Failed**
	- *Curious, I have a feeling I know what is wrong, but will try one more thing before I resort to that.*

**3rd Try**
- Enter Terminal
	- `cd documents`
	- `sudo chmod 700 api-ottawa-mac.sh`
		- `Password: _`
			- `cmod: api-ottawa-mac.sh: No such file or directory`

- Verdict: **Failed**
	- *Issue is stemming from spaces in folder names. Seeking out solutions besides being forced to rename folders.*
	
**4th Try**
- Enter Terminal
	- `cd documents`
	- Googled "folders with spaces in names terminal"
		- Stack Exchange coming in clutch with ["How to cd to a directory with a name containing spaces in bash?"](http://apple.stackexchange.com/questions/14683/how-to-cd-to-a-directory-with-a-name-containing-spaces-in-bash)
			- Decided to try to take the easy route and try the `tab` method suggested
	- `cd Fou `tab becomes: `cd Fourth\ Year./`
		- Note the slashes, if required to enter such folders in manually, either slashes or single or double quotes should be placed around various parts of the command because:
	>bash parses command lines into “words” based on non-quoted whitespace. The cd command typically requires exactly one argument (the destination directory). A command line like cd foo bar means to run cd with two arguments: foo and bar. If you only wanted to send a single foo bar argument, then you need to quote the space:
(e.g.) cd foo\ bar (see more quoting example below). 

	- `cd HIST\ 3907O./` 
		
- Because I have multiple folders that begin with HIST, I actually had to manually input this one
	- `cd API` Tab becomes: `cd API\ Exercise\ Material/`
	- `sudo chmod 700 api-ottawa-mac.sh`
		- `Password:_`
			- `Kathryns-MacBook-Pro:API Exercise Material kathryngreenan$`	
				- Entered wrong password because I accidentally started typing in Terminal when I wanted to type in my notes
	- `cd ..`
		- This takes me back up a directory, so to `HIST 3907O. `
	- `cd API` Tab becomes: `cd API\ Exercise\ Material/`
	- `sudo chmod 700 api-ottawa-mac.sh`
	- `Kathryns-MacBook-Pro:API Exercise Material kathryngreenan$` 
- Verdict: **Fa-WAIT**
		- `./api-ottawa-mac.sh`
			- `% Total	% Received etc`
- Verdict: **Tentative Success**
	- *Data is currently downloading, will be able to judge once script has finished running* (Time is 1:37 PM as of material beginning to download) 
	- As of 2:13 PM, 4179 Pages downloaded... Maybe not accurate?
	- As of 3:03 PM, results.txt file has 84990 lines, with a line before and after each key. 29 lines for 10 keys...
			- I'm pretty sure that means it's pulled around 2930 entries
	- As of 4:28 PM, script has finished running, though not all items were retrieved due to loss of connection
		- Have so far been unable to open up the output.txt file
		
Returning three days later:
- within my API Exercise Folder, I input the command: `sed 's/identifier/\n&/2g' output.txt | split -d -l1 --aditional-suffix=.txt - splitfile`
	- Which proceeded to spit back at me this: `split: illegal option -- d
usage: split [-a sufflen] [-b byte_count] [-l line_count] [-p pattern]
             [file [prefix]]
sed: 1: "s/identifier/\n&/2g": more than one number or 'g' in substitute flags`

            - I'm fairly positive that this is because this command actually contains quite a few placeholder variables that I need to play around with

- Confirmed that `identifier` tag is something that I must replace with my own term based on output.txt... This is suddenly possible after finally realizing the solution to my problem of every application I tried to open my file in crashing.

I realized that opening this large file in a browser was the only way it wouldn't continually crash before loading.

Summary: After over a week, I'm finally back on the horse with this beast. 

### Continuing with Splitting Your output.txt
- Within API exercises folder, trialing command `sed 's/title/\n&/2g' output.txt | split -d -l1 --aditional-suffix=.txt - splitfile` where `/identifier/` has been replaced with `title`
	- Result: `sed: 1: "s/title/\n&/2g": more than one number or 'g' in substitute flags
split: illegal option -- d
usage: split [-a sufflen] [-b byte_count] [-l line_count] [-p pattern]
             [file [prefix]]`
- Trialling `awk '/identifier/{"F"++i;}{print > "newoutput"i".txt";}' output.txt` where identifier is replaced by `<title>`
	- `awk '/<title>/{"F"++i;}{print > "newoutput"i".txt";}' output.txt` 
		- Result: `awk: syntax error at source line 1
 context is
	/<title>/{"F"++i;}{print > >>>  "newoutput"i <<< ".txt";}
awk: illegal statement at source line 1`
- Trialling same script identifier remains in place
	- Result: See above, same error

*As of March 2nd, 2016, I have decided to put a pin in this exercise, as I have so far been unable to split my output file.*

**On Hold**












## Blog Spiel
### I saw the best minds of my generation destroyed by madness, starving hysterical naked

For context, I'm going to link to ["Module 2: or How I Almost Lost My Mind [...]"](https://complexbydegree.wordpress.com/2015/04/04/module-2-or-how-i-almost-lost-my-mind-and-a-major-part-of-the-reason-why-this-entire-thing-is-extremely-late/) from last year, as I am not sure if there's any other way for me to convey the panic and confusion better than the notes I took while trying to complete this exercise last time. It was not fun. It was quite honestly one of the most maddening things I've ever tried to do. 

##### Pre-exercise thoughts: 
Nervous, loaded up with coffee, snacks, and 10+ hours of instrumental music to get me through this. Likewise will be comparing my process to that which I followed last time around, as it's a wonderful resource in what **not** to do.

#### Very early on in the Exercise Struggles
I hit this point: "Now, download api-ex-mac.sh from the repository and save it to your desktop." When I realized that this didn't really make any sense, because this is not the same file as what is linked to in this particular exercise. This was a file from HIST3907B, and I feel that I benefited because I knew that on Dr. Graham's Github, I could access the HIST3907B repository and pull it from there. For some reason I could not figure out how to just download the file, but remembered having this struggle last time which caused a lot of problems because I just tried to copy the program and convince my text editor to save it as a shell script. 
This time, I found the solution pretty quickly, I cloned the repository onto my desktop version of Github, and simply dragged the file to my desktop. 

**Update after reading down 6 lines: shell script was linked, duh**

##### Very Early on in the Exercise Thoughts:   
Cautiously optimistic, hopefully, pleased with things so far, REMIND SELF TO READ ENTIRE EXERCISE BEFORE GOING ON AN ADVENTURE TO FIND RESOURCES OR SOLVE PROBLEMS THAT ARE LINKED FURTHER DOWN THE PAGE.

##### A Week and A Half Later Thoughts:
I still hate APIs with a fiery, burning passion. 