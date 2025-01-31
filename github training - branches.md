---
type: documentation
---
# GitHub Training - Branches

## Foreword

Branching often is something that we hear on a regular basis from everyone in the tech industry and it is something that we have to keep it in our hearts and mind.

---

## What and Why?

Branches are an in-built feature in the Git Versioning System. Consider it a way to make new changes to your code, or your organization's code without deleting everything by mistake. Now we have learned that commits are a way to ensure that we are creating snapshots from time to time when writing some code. It works like time travel in the same Timeline/Universe(Do not get me started on home those two things can be different). Consider the [[Timelines vs Parallel Universe]] Rant.

![](https://i.imgur.com/LsCkQpq.png)

 Here in the above image you can see the different commits made to a project over time, some of them can be bug fixes, some of them are new features, some of them can be extra functionality and then we have the latest commit marked as `release`. What we see here is how a single *timeline* on GitHub would look like.

But alas, that is not how it is, there is something known as ***Git branches***. They are analogous to branches on a tree. Now in a development environment these branches hold the code which is in production and is being constantly worked on, one could have a separate branch for `hotfix`, `features`, `beta` and literally any change that might want to introduce into your repository. 

## Exploring Branches

There are two main different ways to create branches in Git and both of these ways are quite similar to each other. But before we do that, we need to have a Git Repo/Folder with some example commits pre-configured. This is just done for the sake of example and showcasing branching. To learn how to create a a repo, please refer to [[GitHub Training - Basic#Creating a repo| the previous blog.]]

### Creating branches with `git branch`

This is the most easiest and obvious way to create a new branch. We simply use the command,

```bash
#syntax
git branch <branch_name> 

#example
git branch feature1 #this will create a branch named 'feature1'

#If you wish to see the branches that are available
git branch
```

If you follow these commands into your terminal, you will see that you have created a new branch and when using the `git branch` command you will see the number of branches that currently exist in the current repo.

![](https://i.imgur.com/XmZs7oz.png)
 > Note: If you notice there is a `*` marked on `main`. It is to signify that we are currently inside the `main` branch and that we will have to switch to the feature branch if we want to use it.

### Creating branches with `git checkout`

Now the other common method used by many is the use of the `git checkout` command which offers the same functionality with one slight change.

```bash
#syntax
git checkout -b <branch_name> 

#example
git checkout -b feature2 #this will create a branch named 'feature1'

#If you wish to see the branches that are available
git branch
```

Here the commands are mostly the same, but we are using the `checkout` sub-command to create a new branch. What's the difference you may ask, check the below screenshot,

![](https://i.imgur.com/5XrGX4L.png)
> Note: Here you can see that the `*` is marked on `feature2` instead of `main`. Due to the fact that when you use `git checkout`, the new branch is automatically selected.

### Understanding the workflow

#### Step 1
Now let us try to create a dummy project and go through a simple scenario.

```bash
#Creating a new repo
git init website-flow

#Creating some dummy files and commiting them
cd website-flow
echo "<h1>This is my website</h1>" > index.html
git add index.html
git commit -m "Created index.html"

echo "h1, h2, h3 { margin-bottom: 15px; }" > style.css
git add style.css
git commit -m "Created style.css"

#Checking out the logs
git log --all --graph
```

![](https://i.imgur.com/c2VG7Nm.png)

If you notice that I have created two dummy files and along with that made two separate commits to go along with them. Also notice that the latest most commit says `HEAD -> main`. `HEAD` denotes the current pointer position in the commit, imagine that is the current moment in time. `-> main` refers to the fact that we are in the `main` branch at the moment. It will all make sense in a moment, I promise.

> Note: I have used `git log --all --graph` instead of `git log` as we will further see in future, this view is much more useful and intuitive when it comes to branching.

#### Step 2
Now let us try to add a new feature to out code by creating a new branch,

```bash
#creating a new branch
git branch feature1

#checking the branches
git branch

#switching to that branch
git checkout feature1

#checking log
git log --all --graph

```

![](https://i.imgur.com/Vi1S7Hi.png)

As you notice here, we created a new branch and we have switched to it, notice how the `HEAD` now points to `feature1`. Another thing you would notice is that we are on the same commit as the `main` branch and that is because we have not made any changes into any files or staged any commits. Let us do that now.

```bash
#lets ensure that we are in the correct branch
git branch

#creating file new files
echo "feature 0.1" > new_edition.html
git add new_edition.html
git commit -m "added a new feature 0.1"

echo "feature 0.2" >> new_edition.html
git add new_edition.html
git commit -m "modified new_edition.html and added new functionality, feature 0.2"

#Checking out the logs
git log --all --graph

```

![](https://i.imgur.com/Uc3KYEK.png)

We can see that we are in the `feature1` branch and now we have created two new commit that are visible in the logs. Also notice how our `HEAD` now points to `feature1` but we are two commits ahead of our `main` branch.

#### Step 3

Let's see what files are shown in both the branches and see the difference.

```bash
#to see the files in the feature1 branch
git checkout feature1
ls

#to see the files in the main branch
git checkout main
ls

```

![](https://i.imgur.com/EhTSS4i.png)

As you can see, `new_edition.html` does not exist on the `main` branch and it only is limited to `feature1` branch. While we are in the `main` branch, let us try to make a change in the main branch and see how that effects everything.

```bash
#ensuring we are in the main branch
git branch

#making a hotfix in the main branch
echo "hotfix 1.0" >> hotfix.txt
git add hotfix.txt
git commit -m "fixed a bug"

#Checking out the logs
git log --all --graph

```

![](https://i.imgur.com/g3VAqiz.png)

#### Step 4

Now, lets try to checkout what is going on in the `feature1` branch,

```bash
#switching to feature1 branch
git checkout feature1

#checking out the files here
ls

#Checking out the logs
git log --all --graph
```

![](https://i.imgur.com/DZfFGXB.png)

Here we can see if we compare our last two outputs, that we created a new file called `hotfix.txt` in the `main` branch. But when we checked out our `feature1` branch, it was no where to be found. Plus notice the log graph and the `HEAD` position. There are virtually no changes in our `feature1` branch which leads us to the conclusion that changes and commits inside a branch stay there. This workflow is an example of fixing bugs in the `main` branch while keeping out `feature1` branch separate and isolated.


## Syncing with GitHub

Now that we have created these different branches and know enough to play around with them, let's talk about syncing them with GitHub. Hopefully you all remember how we connected Git and GitHub together. If not, you can checkout [[GitHub Training - Basic]]. 

### Connecting `main` branch

This was already covered in the previous documentation, so I will be only posting commands here just in case anyone needs a refresher.

```bash
#adding repo remote to git
git remote add origin https://github.com/amanverasia/website-flow.git

#switching to main branch
git checkout main

#pushing the main branch
git push origin main #we get an error here, we will unpack this later

#performing fetch
git fetch

#trying to push the main branch again
git push origin main #we get an error here again

#trying again but forced update this time
git push origin main -f
```

![](https://i.imgur.com/TjUUMSh.png)

Now what just happened, so we initialized our repository on GitHub first, and it was an empty repository. Then we added it to our Git using the `git remote` command. Everything was going well until we tried to `push` our main branch to upstream (GitHub). Why?

So GitHub considers this a violation because the repository on GitHub is more "updated" compared to the repo that is available locally. Now to mitigate this, and to verify this, we usually perform something known as, `git fetch`, this process downloads the repo from GitHub and makes sure that we are up to date with the version that exists online. In our case, there was nothing to fetch from GitHub, given it was an empty repo. Then we tried pushing the branch again with the switch `-f` to force the push upstream and ignore the warnings.

### Connecting `feature1` branch

Given that we have pushed our `main` branch upstream now its time to do the same for our `feature1` branch. It is a simple command,

```bash
#pushing the feature1 branch
git push origin feature1
```

Now if we perform `git log --all --graph` we will see,

![](https://i.imgur.com/6K6IBpS.png)

that our `HEAD` is at `main` but along with that if you notice we have two more new changes, and that is the introduction of, `origin/main` and `origin/feature1`. Those are basically the last updated pointers that we have when we push/pull/fetch the repo. It will make more sense later on, the more we practice.

## Merging

Creating branches is all fun and games, until it comes to merging branches, now the command to do so is very simple but it requires a lot of logic. Merging of two branches takes place when you are ready to integrate your feature back into the main branch.

Merging happens from the branch you are currently pointed into, meaning if you are say inside the `main` branch, and use the command `git merge` on the `feature1` branch, then the `feature1` branch would merge back into `main`.

```bash
#ensuring we are in the main branch
git checkout main

#merging two branches
git merge feature1 -m "merging feature1 back to main"

#checking the files now
ls
```

![](https://i.imgur.com/eg2BoFO.png)

As you can see, the `new_edition.html` file is now inside our main branch, now if we perform `git log`, we will see the merge in a visual manner,

```bash
#Checking out the logs 
git log --all --graph
```

![](https://i.imgur.com/pJdxMil.png)

As you can see the latest commit at the top has the `HEAD` pointed at `main` and we can see the merge visually. Now sometimes there are can be something known as merge conflicts when we deal with merges, lets look at that.

## Merge Conflicts

Version control systems are all about managing contributions between multiple distributed authors ( usually developers ). Sometimes multiple developers may try to edit the same content. If Developer A tries to edit code that Developer B is editing a conflict may occur. To alleviate the occurrence of conflicts developers will work in separate isolated branches. The `git merge` command's primary responsibility is to combine separate branches and resolve any conflicting edits.

### Understanding merge conflicts

Conflicts generally arise when two people have changed the same lines in a file, or if one developer deleted a file while another developer was modifying it. In these cases, Git cannot automatically determine what is correct. Conflicts only affect the developer conducting the merge, the rest of the team is unaware of the conflict. Git will mark the file as being conflicted and halt the merging process. It is then the developers' responsibility to resolve the conflict.

### Types of merge conflicts

A merge can enter a conflicted state at two separate points. When starting and during a merge process. The following is a discussion of how to address each of these conflict scenarios.

#### Git fails to start the merge

A merge will fail to start when Git sees there are changes in either the working directory or staging area of the current project. Git fails to start the merge because these pending changes could be written over by the commits that are being merged in. When this happens, it is not because of conflicts with other developer's, but conflicts with pending local changes. The local state will need to be stabilized using `git stash`, `git checkout`, `git commit` or `git reset`. A merge failure on start will output the following error message:

```bash
error: Entry '<fileName>' not uptodate. Cannot merge. (Changes in working directory)
```

#### Git fails during the merge

A failure DURING a merge indicates a conflict between the current local branch and the branch being merged. This indicates a conflict with another developers code. Git will do its best to merge the files but will leave things for you to resolve manually in the conflicted files. A mid-merge failure will output the following error message:

```bash
error: Entry '<fileName>' would be overwritten by merge. Cannot merge. (Changes in staging area)
```

### Creating a merge conflict

In order to get real familiar with merge conflicts, the next section will simulate a conflict to later examine and resolve. The example will be using a Unix-like command-line Git interface to execute the example simulation.

```bash
mkdir git-merge-test
cd git-merge-test
git init .
echo "this is some content to mess with" > merge.txt
git add merge.txt
git commit -m "we are commiting the inital content"
```

![](https://i.imgur.com/GNCFVi3.png)

This code example executes a sequence of commands that accomplish the following.

- Create a new directory named `git-merge-test,` change to that directory, and initialize it as a new Git repo.
- Create a new text file `merge.txt` with some content in it.  
- Add `merge.txt` to the repo and commit it.

Now we have a new repo with one branch `main` and a file `merge.txt` with content in it. Next, we will create a new branch to use as the conflicting merge.

```bash
git checkout -b new_branch_to_merge_later
echo "totally different content to merge later" > merge.txt
git add .
git commit -m "edited the content of merge.txt to cause a conflict"
```

![](https://i.imgur.com/otXtN9u.png)

The proceeding command sequence achieves the following:

- create and check out a new branch named `new_branch_to_merge_later`
- overwrite the content in `merge.txt`  
- commit the new content

With this new branch: `new_branch_to_merge_later` we have created a commit that overrides the content of `merge.txt`

```bash
git checkout main
echo "content to append" >> merge.txt
git add .
git commit -m "appended content to merge.txt"
```

This chain of commands checks out the `main` branch, appends content to `merge.txt`, and commits it. This now puts our example repo in a state where we have 2 new commits. One in the `main` branch and one in the `new_branch_to_merge_later` branch. At this time lets `git merge new_branch_to_merge_later` and see what happen!

```bash
git merge new_branch_to_merge_later
```

![](https://i.imgur.com/H24OXvk.png)

That is a conflict. Now what?

### How to identify merge conflicts

As we have experienced from the proceeding example, Git will produce some descriptive output letting us know that a CONFLICT has occured. We can gain further insight by running the `git status` command

```bash
git status
```

![](https://i.imgur.com/dd92QuW.png)

The output from `git status` indicates that there are unmerged paths due to a conflict. The `merge.text` file now appears in a modified state. Let's examine the file and see whats modified.

```bash
cat merge.txt
```

![](https://i.imgur.com/QYFA8mp.png)

Here we have used the `cat` command to put out the contents of the `merge.txt` file. We can see some strange new additions

- `<<<<<<< HEAD`
- `=======`
- `>>>>>>> new_branch_to_merge_later`

Think of these new lines as "conflict dividers". The `=======` line is the "center" of the conflict. All the content between the center and the `<<<<<<< HEAD` line is content that exists in the current branch main which the `HEAD` ref is pointing to. Alternatively all content between the center and `>>>>>>> new_branch_to_merge_later` is content that is present in our merging branch.

### How to resolve merge conflicts using the command line

The most direct way to resolve a merge conflict is to edit the conflicted file. Open the `merge.txt` file in your favorite editor. For our example lets simply remove all the conflict dividers. The modified `merge.txt` content should then look like:

```bash
this is some content to mess with
content to append
totally different content to merge later
```

Once the file has been edited use `git add merge.txt` to stage the new merged content. To finalize the merge create a new commit by executing:

```bash
git commit -m "merged and resolved the conflict in merge.txt"

git log --all --graph
```

![](https://i.imgur.com/MW0j0ME.png)


Git will see that the conflict has been resolved and creates a new merge commit to finalize the merge.

### Git commands that can help resolve merge conflicts

#### General tools

```undefined
git status
```

The status command is in frequent use when a working with Git and during a merge it will help identify conflicted files.

```bash
git log --merge
```

Passing the `--merge` argument to the `git log` command will produce a log with a list of commits that conflict between the merging branches.

```bash
git diff
```

`diff` helps find differences between states of a repository/files. This is useful in predicting and preventing merge conflicts.

#### Tools for when git fails to start a merge

```bash
git checkout
```

`checkout` can be used for _undoing_ changes to files, or for changing branches

```bash
git reset --mixed
```

`reset` can be used to undo changes to the working directory and staging area.

### Tools for when git conflicts arise during a merge

```bash
git merge --abort
```

Executing `git merge` with the `--abort` option will exit from the merge process and return the branch to the state before the merge began.

```bash
git reset
```

`Git reset` can be used during a merge conflict to reset conflicted files to a know good state

## Deleting Branches

Once you’ve finished working on a branch and have merged it into the main code base, you’re free to delete the branch without losing any history:

```bash
git branch -d crazy-experiment
```

However, if the branch hasn’t been merged, the above command will output an error message:

```bash
error: The branch 'crazy-experiment' is not fully merged. If you are sure you want to delete it, run 'git branch -D crazy-experiment'.
```

This protects you from losing access to that entire line of development. If you really want to delete the branch (e.g., it’s a failed experiment), you can use the capital `-D` flag:

```bash
git branch -D crazy-experiment
```

This deletes the branch regardless of its status and without warnings, so use it judiciously.

The previous commands will delete a local copy of a branch. The branch may still exist in remote repos. To delete a remote branch execute the following.

```bash
git push origin --delete crazy-experiment
```

or

```bash
git push origin :crazy-experiment
```

This will push a delete signal to the remote origin repository that triggers a delete of the remote `crazy-experiment` branch.

## Ending Thoughts

Now that you know how to create, merge and delete branches you can go ahead and create something new and functional and test out the limits of the limitless functionality provided by Git. In the next post we will be learning about ***GitFlow*** and ***Pull requests***.