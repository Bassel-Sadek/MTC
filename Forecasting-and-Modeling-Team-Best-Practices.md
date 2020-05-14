
# Background

There are a number of practices I've found useful over the years in creating code/scripts.  In thinking about my motivation for these practices, I think they serve to:
* facilitate collaboration by making code/script easier for others to use and understand
* enable us to reproduce results (or results with small variants)

# Source Control 

* *Clear commit comments*: `update scripts` or `code cleanup` are not useful commit messages because if someone is trying to find a revision before a particular change was made, they would need to read the entire commit.  The commit comment should be more specific -- what's the effect of the update or cleanup?  Does it change results?  And ideally, the diff should be helpful too -- so when making a bunch of functional changes, I think it can be helpful to do one functional change, and commit it once it's working, and then the next in another commit.

* *Commit before sharing output*: When multiple people are working on a project at the script change is good enough to post the results in a common location (e.g. Box or a shared drive or wherever the shared outputs get posted), then the script update should be committed.  Otherwise, people may be looking at output that is out of sync with their version of the script/code, which is confusing.
