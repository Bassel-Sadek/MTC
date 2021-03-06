[[Home]] > [[TravelModel]]

***

To promote model transparency and to help with future debugging of modeling results, we recommend making the following requirements part of consultant contracts which develop custom (e.g. agency) variants of an MTC model (including custom calibrations, version with alternate input datasets or components, etc.):
* When model development begins, a fork of the MTC model should be made for the development effort; this makes it clear which model version is the basis of the development.  Ideally, this fork would be in the agency GitHub organization, but a personal or consultant GitHub organization can be used instead, as long as the repository is public.
* All model code, script, UEC changes or config should be committed to that GitHub fork _as work progresses_.  Do not commit a single giant commit of all changes to files at the end, since this makes it hard to understand how the changes evolved.
* Commits should include useful commit messages (e.g. say what the commit does. For example, "fix bug where X was happening", rather than "update file X"
* At the completion of the work, a pull request should be issued to the MTC repository, to create a new branch for the agency version of the code.  The pull request should include a summary of the changes made to the agency variant of the code.


![](https://github.com/BayAreaMetro/modeling-website/blob/f7df6460b56860b08509533b7f6e677f0ed3a22b/foswiki_imgs/LokiVariant.jpg)