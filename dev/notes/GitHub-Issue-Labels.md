We try to use a standard set of labels across all the NUnit repositories. In some cases, an individual project may not yet have been converted to use these labels, but we expect to do so soon.

That said, don't stress about whether something is a bug or an enhancement, normal versus low priority, etc. Just pick one. If things change later, the label can be changed as well. This is only intended to help us organize a relatively large number of issues, not to give us extra work.

####What it is
Labels starting with **is:** indicate the nature of the issue. Only one should be used, based on the judgement of the committer who assigns the label. If there is no **is:** label, then we presumably don't know what the item is and should not be working on it!
* **is:bug** Something that isn't working as designed.
* **is:docs** Solely pertaining to the documentation or sample code.
* **is:enhancement** An addition or improvement to an existing feature.
* **is:feature** An entirely new feature.
* **is:idea** An idea about something we might do. We discuss these until they are either dropped or turned into a feature or enhancement we can work on.
* **is:question** Just a question - we discourage these as issues but they do happen.
* **is:build** Something to do with how we build the software, scripts, etc.
* **is:refactor** What it says: refactoring that is needed.

####Priority
Labels starting with **pri:** indicate the priority of an issue. Pick just one, please. Priority may, of course, change over time, as items become more or less important to us. If no priority is assigned, we shouldn't be working on it.
* **pri:critical** Should only apply to bugs, which need to be fixed immediately, dropping everything else. At times, we will even speed up the release cycle due to a critical bug.
* **pri:high** High priority - implement as soon as possible.
* **pri:normal** Standard priority - implement when we can.
* **pri:low** Low priority - implement later or not at all.

####Ongoing Status
Labels starting **status:** indicate the status of an open issue. There should only be one of these per bug and they may be removed when bugs are closed - however, leaving the last one there does no great harm.

####Close Status
Labels starting with **closed:** indicate the status of the bug at closing and should only appear on closed bugs. Please remember to apply one of these when closing a bug as it makes it easier to review the list of closed bugs without opening each one to see what the disposition was.
* **closed:done** The work called for is done, i.e. the bug is fixed or the feature/enhancement is implemented.
* **closed:duplicate** The issue is a duplicate of one that we are working. A comment should indicate the issue number.
* **closed:notabug** The issue (generally a bug) is not valid or the feature already exists. There should be an explanatory comment.
* **closed:norepro** While the issue (generally a bug) may exist on the user's system, we have tried and are unable to reproduce it. If somebody later figures out a repro, the issue can be reopened.
* **closed:wontfix** The issue is possibly valid but we don't intend to implement it. It may be out of scope for the project or inconsistent with the values and priorities of the project. There should be an explanatory comment.

####Other Labels
* **confirm** Somebody should verify that the issue actually exists and then remove the label. In some cases, a bug may have been reported against an older version of NUnit and needs to be checked out using the current code.
* **blocked** The issue cannot be worked on until something else happens, external to the project. There should be a comment on the issue indicating what that something is.
* **design** Some design decisions need to be made before this can really be worked on. Sometimes this label may be applied before anything happens and other times the work may have started but reached a point where design decisions need to be made involving others in the team.
* **easyfix** Indicates an issue that might be a good place for a new contributor to start. Whoever adds the label should couple it with a comment suggesting what code to look at and a general approach to working the issue.
