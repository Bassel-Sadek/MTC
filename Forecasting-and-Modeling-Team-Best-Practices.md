[[Home]] > [[Forecasting and Modeling Team Best Practices]]

***

See also [Guidelines for Developing Variants of the MTC Travel Model(s)](Guidelines-for-Developing-Variants-of-the-MTC-Travel-Model(s))

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

* **Describe the work completed and verification tests in a Pull Request**: A basic explanation of the changes made in a PR is a useful way to document chunks of work completed (big or small). The explanation helps future folks looking at the code quickly understand what occurred, and helps the contributor remember the work completed as well as any context for it not visible through the code alone. Even more helpful is a quick report of what was done to verify that the code is working. This can include the environment used to produce the results, and any tests run along with their outcome. For changes that are not meant to affect results, two comparative runs are a useful verification. 

# Workflow

* **Use branches and pull requests to make changes**: Branches allow work to be done without changing the master version of a repository. Using a branch makes it so that changes to the model for a specific purpose can be tracked. With multiple contributors on a project (or model), different streams of work need to be reviewed to ensure that many moving parts work together. Using pull requests creates a history of the work done in a particular area that becomes very important in understanding changes (big or small) to the model from many sources. Because they keep draft work and changes away from master, branches also ensure that any contributor can branch off of master at any time, and the model will be functioning as needed. 

* **Merge master into branches often**: While development work is kept in branches, changes that have been reviewed and are complete get merged into master. In order to keep branches up-to-date with the latest changes to the model, branches should merge in changes from master often- for example, each time you start working in your branch. Doing so ensures that the work being completed in a branch is in tune with any changes to the model, and won't have to be re-worked when merged. It also reduces issues when branch-to-branch merges or other configurations are needed. Similarly, if work is being submitted to a staging branch, master should be merged into that work before creating a PR to the staging branch. 

* **Only modify your own branches**: This one is more concerned with branch workflow than collaboration within a branch. When reviewing, testing, and pulling in work from a branch, it can be tempting to modify the work done in that branch. However if you're not the owner of that branch, this can confuse the workflow.

* **Make changes to the source branch rather than a staging branch**: Similar to using using branches rather than committing directly to master, when a staging branch exists it's best to make changes in a branch rather than commit directly to the staging branch. It can be tempting to make changes directly to the staging branch after merging a branch in, but using the applicable branch allows streams of work to be tracked. For the person maintaining the staging branch, this also helps ensure that contributors make changes to their own branches, rather than have their work changed unknowingly in the staging branch (see: only modify your own branches). 

* **Test code when changes are made**: Whenever code is submitted to be merged into the codebase, the contributor should verify that the code performs as intended so as to not degrade the codebase. This often involves checking that the code produces the intended results and/or output, and adding print statements is an important way to check that the intermediate steps (or lines of code) are working. In addition, it should be the confirmed that a full simulation runs without errors, since indirect errors can result from changes elsewhere in the code (there are ways to reduce the need for this that should continue to be explored). On the other side, a complete review would mean that the person reviewing the PR also runs the code to confirm that it is working, and then merges the pull request. 

# Regional Transportation Plan Travel Model Runs

* Scripts that are run with output used as a deliverable *must be committed to [travel-model-one on GitHub](https://github.com/BayAreaMetro/travel-model-one) as **current***.  If a bug is discovered in a script and the script is patched, the patch must be committed to Github.

* Duplicate or undocumented script directories (e.g. `emfac2`, `emfac3`) are unacceptable because they cause confusion and obfuscation (e.g. what is the problem with `emfac`?  What is the difference between these directories?). 
  * If a bug was discovered with the a script in the original directory, the fix should be *committed to GitHub* and applied to the correct directory.  Unless there is a compelling (and documented) reason, incorrect scripts/output should not be left to cause confusion.
  * If another directory is required, the reasons need to be documented and the naming of that new directory needs to be clear (e.g. `emfac_without_trucks` to clarify how it differs from the original `emfac`). Additionally, a `Readme.txt` file needs to be added to the new directory explaining or linking to an explanation of the contents of this directory so that other users of the model run don't need to diff all the scripts/output to understand the contents of the directory and how it differs with the original.

* Model outputs that have been used for official purposes (e.g. summary files, EMFAC outputs) should be copied to the relevant `OUTPUT` folder on the *M Drive* because the directories on modeling machines are not backed up or considered permanent storage.