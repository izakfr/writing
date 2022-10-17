# On Git

Sharing code is an essential part of programming. When you work with others, it is likely that you will both modify code within the same application.
When sharing code, there are a few options. Hypothetically, you could email your files back and forth. This is a terrible idea. There is no way to determine which version is the most up to date version and there's no way to see any edit history. If projects were run like this, it would be difficult for even two people to coordinate, let alone more. A better solution, is to use a centralized repository where there is one copy of the code that everyone can see and interact with. Centralizing the code solves the issue of not having a "source of truth" for the code. The code that lives in this centralized location is considered the up to date version.

Writing code is difficult. One of the worst things that can happen to you is to write code that doesn't work. Something worse than that is to use someone else's code that doesn't work. Situations like that can lead to frustrating debugging sessions and wasted hours. These situations can be remedied by treating the centralized code store as sacred. Whatever code lives in the centralized location is assumed to be correct and working at all times. If this is not the case, it can be catastrophic to all developers using it. In Git language, this centralized code source is usually called the master branch. The master branch is to be valid at all times and no one is to break it. The definition of broken usually includes failing test, failing linters, incorrectly implemented features, etc. Given that the master branch is always assumed to be valid, as developers, we can assume no issues when working off of this code version.

At some point, of course, we will want to modify the features that exist on the master branch. This process starts with creating a new branch off of master. When we create this new branch, it will be an exact copy of the master branch. At this point, we can make local changes to the files we have. At some point, when the local changes are finished we will want to add our changes to the master branch, and solidify them as "valid". To do so, we can create a commit and push our changes to the shared code repository. At this point, another developer will see two versions of the code in the shared repository. The "valid" version (aka master branch) and our suggested changes (our feature branch). To kickoff the process of entering our code into cannon, we must create pull request. To open a pull request is to claim that my code changes are ready to be considered valid, and should be adopted by others. If the other people working on the project agree, they will approve your pull request. This is the green light to go ahead and make your changes valid by moving them into the master branch.

Let's say we make some changes to the code and our version becomes valid when we move it to the master branch. Then at some later point, others come in and make modifications and also move their code to master. When we look at the code now, we see a snapshot of what the valid code is. While this is useful, it is also necessary to see the evolution of the code. It is useful to see what changes were made since our last change. This history of changes is just a list of commits. Each commit represents a change of the code from one version to another. Appended together, these commits represent the current state of the code.

Imagine we have a timeline of our life that details every single hour of the day for the duration of our lifetime. This timeline would not be useful at all. If I wanted to read about a specific event I would have to turn through thousands of pages just to find a few details. A better timeline is one that breaks each key event into a discreet point and lays them out in order. If I wanted to find my 10th birthday,  I would just search for 10th birthday in the timeline. This timeline example parallels to a history of Git commits. If I have a history of every single line change, each in its own commit it wouldn't be useful. How then, should we divide up commits? Going back to the timeline, we can divide each commit into a discreet feature. This isn't a perfect prescription, but it is a good heuristic. Each commit, should be a standalone feature that meaningfully adds (or removes) something to the code.

To summarize, here are some rules to follow when working on shared git projects:
- The master branch is always valid (given it's not broken)
- If the master branch is broken revert commits that invalidated it
- Always work locally off the valid branch (master)
- Break up commits into discreet features
- Always get commits reviewed before moving them to master
- Move your commits onto master as frequently as possible
- Commits cannot be moved onto master from a branch that is behind master

Here is a example workflow for making changes:
```
// STEP 1: create local branch
git checkout master
git pull
git checkout -b feature-add-new-feature

// STEP 2: make local branch
git commit -m "Add change 1"
git commit -m "Add change 2"
git commit -m "Add change 3"
git push --set-upstream origin feature-add-new-feature

// STEP 3: create pr on git repo site
// create pull request
// get pull request approved

// STEP 4: rebase onto master
git checkout master
git pull
git checkout feature-add-new-feature
git rebase master
// resolve conflicts

// STEP 5: squash commits and push
git rebase -i HEAD~3
// select squash for all commit execpt the earliest
// ammend commit message to summarize entire feature change
git push --force

// STEP 6: merge
git checkout master
git merge --ff-only feature-add-new-feature
git push

// STEP 7: delete branch as cleanup
git push origin -d feature-add-new-feature
git branch -d feature-add-new-feature
```
