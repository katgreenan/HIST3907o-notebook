## The Dream Case

"In the dream case, your data are not just images, but are actually sorted and structured into some kind of pre-existing database. There are choices made in the creation of the database, but a good database, a good project, will lay out for you their decision making, their corpora, and how they've dealt with ambiguity and so on. You search using a robust interface, and you get a well-formed spreadsheet of data in return. Two examples of 'dream case' data:
 - [Epigraphic Database Heidelberg](http://edh-www.adw.uni-heidelberg.de/inschrift/suche)
 - [Commonwealth War Graves Commission, Find War Dead](http://www.cwgc.org/find-war-dead.aspx)
 
 ### Instructions
 
In the CWGC database, search your own surname. Download your results. You now have data that you can explore! In your online research notebook, make a record (or records) of what you searched, the URL for your search & its results, and where you're keeping your data

### The Details

I'm storing my data in my course folder on my machine, but will also likely be duplicating it to my Github folder so that it will be in my repository. 

Searching: 'Greenan':
http://www.cwgc.org/find-war-dead.aspx?cpage=1

Searching 'Willis':
http://www.cwgc.org/find-war-dead.aspx?cpage=1

**Complete**

#### Blog Post or Section of One Follows

I promise I've left these links visible for a reason. See, when you enter a search term, no matter what that search term is, you get the same URL. If you, as someone reading this, were to click on either of those links, it will automatically link you to the "Find War Dead" homepage. I tested this by opening the link in a 'private' window, to prove my hunch that this site uses cookies to determine what to show you when you click that link. When I pasted it again into my standard window, it showed me the results of my previous search for 'Willis.'

So, what's a girl who wants to show off her data within the well-designed web framework she found it in to do? Open the developer tools and pretend that she knows what's going on, of course!

(Excluding one or two times that I have been following an explicit tutorial on something, I have never used the developer tools, as a heads up.)

The answer, as far as I can tell, is that there is not a secret, hidden URL that will lead someone directly to my specific search. This is because, unsurprisingly, the content creators did not sit down and write out a code that explicitly details every possible surname you could possibly input - and it makes sense, when you think about it. It makes significantly more sense to do exactly what was done, and code for placeholders and classes, so when things are written in those boxes, the program will read that you have filled this out, and replace the placeholder/class with what you typed. i.e. 	
							`<div class="dottedBoxContainer">
								<div class="dottedBoxContent">`
                                    
                                    `<p>You have searched for  Surname: <span class="searchTerm">Willis</span>
                                    

									<div class="buttonContainer searchActions floatRight">
                                        <input type="submit" name="ctl00$ctl00$ctl00$ContentPlaceHolderDefault$cpMain$ctlCasualtySearch$btnNewSearch" value="New search" id="ContentPlaceHolderDefault_cpMain_ctlCasualtySearch_btnNewSearch" class="redButton" />

                                        
										
                                        
										
									</div>
								</div>
							</div>`
							
As found between lines 925-940 on the Resources tab of my developer window. This is showing my own search term replacing the placeholder. 

Despite knowing only basic HTML and Markdown, I found it really interesting to scroll through the source code of this page. I found I understood a whole lot more than I expected to about what was going on, and feel like examining the source of somewhat simple sites like this in conjunction with the work I've been slowly doing on [Code Academy](codeacademy.com) would really accelerate my understanding of various programming languages. 
 
