### Setting up your Github space

#### Get Git: Configure Git

Lo, of course I run into issues right off the bat, as upon verifying that I had set up git correctly, I was greeted by an error Error: Command failed: /bin/sh -c git config user.email Agreeing to the Xcode/iOS license requires admin privileges Commence flashbacks and the horror of trying to get HomeBrew installed from last year. Luckily I stayed my head, and simply searched the error online. Turns out it's become pretty common with new iterations of OS X, and all that's needed to circumvent this is to manually open Xcode (can be found via Launchpad) and accept the new user agreement.

#### Git-it: Branches Aren't Just For Birds

Oh dear, I have no idea why this beast posed such a problem to me. It pushed back my work schedule by several days because despite someone else having the exact same issue as me and having it revolved in our Slack channel, I *could not* figure out what I was doing wrong! Thus, every day, I'd make a little bit of head way towards figuring out what was wrong. 

 - Day One: Figured out quickly on my own that the <> symbols do not and should not be entered into my own commands
- Day Two (upon someone else running into the same issue: Realized I'd named all my things just my Github username, not add-USERNAME like I needed to, change branch and .txt file names
- Day Three: Bash head into wall, repeat.
- Day Four: Delete cloned repo, clone again, things seem to go swimmingly until things just stop working...
- Day Four (Post Rejuvenating Snacks): Realize quotation marks in tutorial are superfluous, adjust command and get: 
`fatal: 'orgin' does not appear to be a git repository
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.`   

Proceed to grumble, and then decide to check my Github account online to see if I can figure anything out... Turns out, my first mistake, where I named everything "USERNAME" instead of "add-USERNAME" was still haunting me, while this change was showing in my terminal, the change wasn't reflected on my actual repo. 
Solution? Delete my forked copy of the repository, re-fork... basically re-do the entire exercise plus the one before it - and hey, presto! There we go!

**COMPLETED**
