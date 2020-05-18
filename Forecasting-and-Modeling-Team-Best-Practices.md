[[Home]] > [[Forecasting and Modeling Team Best Practices]]

***
# Background

There are a number of practices I've found useful over the years in creating code/scripts.  In thinking about my motivation for these practices, I think they serve to:
* facilitate collaboration by making code/script easier for others to use and understand
* enable us to reproduce results (or results with small variants)

# Source Control 

* **Communicate effects of commit in the commit comment**: `update scripts` or `code cleanup` are not useful commit messages because if someone is trying to find a revision before a particular change was made, they would need to read the entire commit/diff to understand the effect of the change.  The commit comment should be more specific -- what's the effect of the update or cleanup?  Does it change results?  And ideally, the diff should be helpful too -- so when making a bunch of functional changes, I think it can be helpful to do one functional change, and commit it once it's working, and then the next in another commit.

* **Commit before sharing output**: When multiple people are working on a project at the script change is good enough to post the results in a common location (e.g. Box or a shared drive or wherever the shared outputs get posted), then the script update should be committed.  Otherwise, people may be looking at output that is out of sync with their version of the script/code, which is confusing.

* **Use `.gitignore` to ignore files that shouldn't be committed** e.g.
  * [`.DS_Store`](https://en.wikipedia.org/wiki/.DS_Store)
  * `.RData`

* **Include file versions in commits**: For files in a repository that get updated, it can be very difficult to track which file is currently being used without storing some information about where it came from and its version. When an updated file is committed, a good place to store that information is in its commit. If the file came from another repository (eg regional_forecast, travel model, BAUS) you can link to the commit or location where that file was added to its source repository. 

# Workflow

* **Always use branches to make changes**: Branches allow work to be done without changing the master version of a repository. Using a branch makes it so that changes to the model for a specific purpose can be tracked, but they can also be reviewed this way. With multiple contributors on a project (or model), different streams of work need to be reviewed to ensure that many moving parts work together. By using branches and pull requests this can happen, which also creates a history of the work done in a particular area (becomes very important in understanding what has been done to the model). In addition, it ensures that any contributor can branch off of master as needed, and the model will be functioning as needed. 

