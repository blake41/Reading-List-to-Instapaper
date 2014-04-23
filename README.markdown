# Reading List to Instapaper
[blog.ryantoohil.com](http://blog.ryantoohil.com/2012/03/using-safaris-reading-list-to-feed-instapaper.php)

## Intro
[Instapaper](http://www.instapaper.com) is great and I use it all the time. The bookmarklet works fantastically on the desktop, but not as well in iOS (particularly on the iPhone). The issue on the iPhone is that, to execute the bookmarklet, you have to navigate back up your bookmarks to find it.

It's a lot easier to use Safari's built in "Add to Reading List" which is right in that little "Send" icon in the chrome.

This little script attempts to bridge the gap and let you use Safari's Reading List (and the nifty quick icon in iOS, as well as Shift-CMD-D in Safari) to add items to your Reading List, that get automagically added to Instapaper.

A couple of notes: I'm not a great Rubyist, so this code is probably cringe-incuding to most folks. Feel free to turn it into 10 beautiful lines of code. But, hey, this works, right? It'll only work on the Mac, but I'm sure someone can figure out how to make it work on Windows (does Windows Safari have the Reading List?).

## Setup
* Clone the repo
* chmod +x readinglist_to_instapaper.rb
* Open readinglist_to_instapaper.rb and edit the credentials to be your Instapaper credentials
* Install the necessary gems. I should include a gemfile or something. I'll do that at some point.
* Open com.ryantoohil.readinglisttoinstapaper.plist and change the paths to match your paths (the path to the ruby script, and the path to your Safari Bookmarks.plist). This should be pretty obvious. 
* launchctl load <plist file>. This will load up the plist as a launchagent.

That should pretty much be it. Open up Safari and add something to the Reading List. A few seconds later, you should see a little Growl popup (assuming you have Growl installed) that tells you if it succeeded to add the article.

I'll clean this up as I go. Please feel free to add issues or pull requests. I have little idea what I'm doing, but I'll do my best to incorporate them.

## Revisions
* Mar 31, 2012: Initial Commit
* May 6, 2012: Removed rails dependency and cleaned up DateTime usage. I think.

## Blakes Notes
* the file we want to run from the launchctl is _rvmruby
* that script should be a bash script which loads rvm as a function into the shell
* it should take arguments from the plist file as to what version of ruby it should use
* it should take arguments as to the absolute path of the actual ruby script
* all gems need to be installed in that version of ruby
* the _rvmruby file must have the correct permissions set
* you must load the script first (launchctl load com.ryan...)
* then you have to actually run it (launchctl start readinglisttoinstapaper)
* check the exit code to make sure its 0
* if the rvmruby script cant run you wont get any debug output
* once that is running you can add debug info to the shell script
* once the ruby script is running you can get debug output in the ~/Documents/Readinglist.err and .out
* the plist file should go in the /Users/blake/Library/LaunchAgents
* 