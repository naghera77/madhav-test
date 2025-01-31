---
type: documentation
---

# GitHub Training - Basic

## What is GitHub?

GitHub is a website and cloud-based service that helps developers store and manage their code, as well as track and control changes to their code.


## Git vs GitHub

Git is the version control software that can help you keep a history of your commits and features that you make in code. On the other hand GitHub is something that facilitates and allows for that functionality.

Think in terms of Videos and YouTube, 
1. let's imagine that you are filming a short movie (your project).
2. You are recording different scenes (Git commits).
3. Editing them as you go along (Git Tracking your changes).
4. Now you decide that you want to change something in the last scene and so you want to go back to an earlier version (Git Resets and Rollback).
5. You upload your finished movie to YouTube (pushing your project to GitHub)
6. You invite others to watch your movie and suggest edits (collaboration on GitHub)

When you think about it, at the end of the day, GitHub is just a place for developers to get together and manage their code in a better way.


## Basics of Git

Now since all of you are developers, I am gonna continue from now on, with the assumption that you guys are aware about basic coding terms.

### Installing Git
Let's start with setting up Git onto your computer, now most of you would have a pre existing installation of Git, in that case, feel free to skip this step and move on ahead to the next sub-topic.

Depending on what operating system you have, please check the below instructions.

#### Windows
1. Download the [latest version of Git](https://git-scm.com/download/win) and then run the installation with Administrator Rights.
2. Choose an appropriate installation location (default is fine).
3. Install the default components, including Git GUI and Git Bash.
4. Choose your preferred Git default editor. (Sublime Text, VSCode or Notepad++ should be more than fine).
5. Add Git to the Windows PATH.
6. Accept the default line ending conversion for Unix and Windows compatibility.
7. Chose the extra option to enable system caching.
8. Click Finish to complete the install.
9. Open powershell and type `git --version` to confirm installation.

#### Linux
##### Step 1: Update the system

Run these commands in the terminal to update the Linux system:

```bash
sudo apt update
sudo apt upgrade
```

##### Step 2: Install Git
You likely have `git` installed already, but to make sure that we have the most up to date version of git, run the following commands:

```bash
sudo add-apt-repository ppa:git-core/ppa
sudo apt update
sudo apt install git
```

##### Step 3: Verify version

Make sure your Git version is **at least** 2.28 by running this command:

```bash
git --version
```


#### MacOS (ARM/Intel)
##### Step 0: Install Homebrew

First, you’ll need to install Homebrew. Make sure you have checked the requirements [here](https://docs.brew.sh/Installation#macos-requirements). Once you meet the requirements, copy and paste the following into your terminal:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

> On an Apple Silicon Mac you will have an extra step to take. If you look at the terminal output after installing Homebrew, you will see “Installation Successful!”. Further down in the terminal there will be a section called “Next steps”. Reading the terminal may seem a bit intimidating, but this is a great chance to overcome those feelings. Follow the next steps as stated in your terminal (copy and paste the commands given) to add Homebrew to your PATH, which allows you to use the `brew` command prefix.

##### Step 1: Update Git

MacOS already comes with a version of Git, but you should update to the latest version. In the terminal, type

```bash
brew install git
```

This will install the latest version of Git. Easy, right?

##### Step 2: Verify version

If you have just installed and/or updated Git from the previous step, first close that terminal window.

**Open a new terminal window** and then make sure your Git version is **at least** 2.28 by running this command:

```bash
git --version
```

If the version number is less than 2.28, follow the instructions again. If you are encountering a `no formulae found in taps` error:

1. Run `brew doctor`.
2. You will see an output like the one below. NOTE: The actual output of `brew doctor` may vary based on the version of MacOS you’re running, and any other issues you may have with your own installation. Ultimately, you must run each command line snippet that Homebrew provides after running `brew doctor` to repair your installation of Homebrew, including `brew cleanup` at the end. [![Brew Doctor Sample Output](https://cdn.statically.io/gh/TheOdinProject/curriculum/284f0cdc998be7e4751e29e8458323ad5d320303/foundations/installations/setting_up_git/imgs/00.png)](https://cdn.statically.io/gh/TheOdinProject/curriculum/284f0cdc998be7e4751e29e8458323ad5d320303/foundations/installations/setting_up_git/imgs/00.png)
3. Run `brew install git`, **open a new terminal window**, and then check your version of Git, which should now be the latest.


### Configure Git and GitHub
##### Step 1: Create a GitHub account

Go to [GitHub.com](https://github.com/) and create an account! During the account setup, it will ask you for an email address. This needs to be a real email, and will be used by default to identify your contributions. If you are privacy conscious, or just don’t want your email address to be publicly available, make sure you tick the following two boxes on the [Email Settings](https://github.com/settings/emails) page after you have signed in:

[![GitHub Email Settings](https://cdn.statically.io/gh/TheOdinProject/curriculum/770be14190139683dbe9933ca5e9393c797c63f2/foundations/installations/setting_up_git/imgs/01.png)](https://cdn.statically.io/gh/TheOdinProject/curriculum/770be14190139683dbe9933ca5e9393c797c63f2/foundations/installations/setting_up_git/imgs/01.png)

Having these two options enabled will prevent you accidentally exposing your personal email address when working with Git and GitHub.

You may also notice an email address under the **Keep my email addresses private** option, this is your private GitHub email address. If you plan to use this, make note of it now as you will need it when setting up Git in the next step.

##### Step 2: Create a Token
Go to [GitHub Profile Settings](https://github.com/settings/profile) and on the side bar on left, scroll down and click on [Developer Settings](https://github.com/settings/apps). This page gives you access to all of the GitHub apps and all the Tokens that you can make. When you click on ***Personal access tokens*** you will see two options,
- Fine-grained tokens
- Tokens(classic)

Fine-grained tokens allow for more control over the scope of the data and work, but they are in *beta* and thus does not offer the functionality that we require. We shall be moving forward with *Tokens(classic)*.

Click on ***[Tokens(classic)](https://github.com/settings/tokens)*** and there you would be able to see your existing tokens, you can see when they were last used and you can also revoke them, incase of a **security incident** where you might feel that your token is revealed.

Clicking on *Generate new token*, select ***Generate new token(classic)***, put in your 2FA if prompted. Name your token something descriptive, and then set the expiration to 90 days.

Now comes the part where we select the relevant scopes, `repo`, `workflow`, `admin:org/read:org` and `gists`

![](https://i.imgur.com/Ix0tzoz.png)


At the bottom, click on *Generate Token* and then copy the token for use.
> Note: Please store the token somewhere safe, as it is only shown to us **one time** and there is no other way to reveal the token again. We can regenerate the token but all the applications and scripts (in our case, GitHub cli) would need to be configured again.

##### Step 3: Setup Git

For Git to work properly, we need to let it know who we are so that it can link a local Git user (you) to GitHub. When working on a team, this allows people to see what you have committed and who committed each line of code.

The commands below will configure Git. Be sure to enter your own information inside the quotes (but include the quotation marks)!

```bash
git config --global user.name "Your Name"
git config --global user.email "yourname@example.com"
```


GitHub recently changed the default branch on new repositories from `master` to `main`. Change the default branch for Git using this command:

```bash
git config --global init.defaultBranch main
```

To enable colorful output with `git`, type

```bash
git config --global color.ui auto
```


To verify that things are working properly, enter these commands and verify whether the output matches your name and email address.

```bash
git config --get user.name
git config --get user.email
```

> **macOS Users:** Run these two commands to tell Git to ignore .DS_Store files, which are automatically created when you use Finder to look into a folder. .DS_Store files are invisible to the user and hold custom attributes or metadata (like thumbnails) for the folder, and if you don’t configure Git to ignore them, pesky .DS_Store files will show up in your commits. Remember to copy and paste each of these commands into your terminal.

```bash
echo .DS_Store >> ~/.gitignore_global
git config --global core.excludesfile ~/.gitignore_global
```

##### Step 4: Adding Token to Git
Now that we have Git configured onto our local system, we can do a lot of things locally onto our machines, and I am pretty sure that most of you are familiar with commands like, `git add`, `git commit`, `git push` and so on. But before we explore that, we will configure our token that we created in [[#Step 2 Create a Token | Step 2]]. For that, we will be again using bash commands into our terminal, so let's ensure that we have a fresh terminal open.

The first order of business is to verify our current username and email stored in the local Git. To do that, we use the following commands,
```bash
git config --get user.name
git config --get user.email
```

If the values represented are not what you want, please follow [[#Step 3 Setup Git | Step 3]] and configure your Git.

Now we need to create a secure store of our credentials using the `git credential approve` command.

Use the below command template, edit out your own values and then paste it into your terminal.

```bash
git credential approve <<'EOT'
url=https://github.com
username=<your-username>
password=<your-token>
EOT
```

> Please make sure that there are no trailing spaces in the command or else it will cause url-encoding issues, and you will be seeing `%20` into your credentials file. To mitigate that, below given is a one liner which accomplishes the same results.

`git credential approve <<< $'url=https://github.com\nusername=<your-username>\npassword=<your-token>'`


Here is an example using my own credentials,

```bash
git credential approve <<'EOT'
url=https://github.com
username=amanverasia
password=ghp_27p7UZzWPKgfdY2YfE6f9dsTUqXSlv2Wlj4m
EOT
```
> Do not worry, this isn't my actual token.

One Liner,
`git credential approve <<< $'url=https://github.com\nusername=amanverasia\npassword=ghp_27p7UZzWPKgfdY2YfE6f9dsTUqXSlv2Wlj4m'`

You can verify that the file exists and then open it using,
```bash
ls -a ~/
cat ~/.git-credentials
```

![](https://i.imgur.com/kdg9phT.png)

If you ever need to revoke the old credentials or delete the file for some reason, you can use,
```bash
rm ~/.git-credentials
```

That's it! With that our Git is perfectly configured with our GitHub account, and now we can do fun things.


### GitHub Workflow
We will be going through a very basic workflow of actions in GitHub, to familiarize you with the platform.

#### Creating a repo
The first and foremost step that we will be performing is creating a GitHub Repo online. First we will visit, [GitHub Website](https://github.com/), login to our account if not already done so. Then create a new repository by clicking the button shown in the screenshot below.

![](https://i.imgur.com/8Nm4Vhv.png)

Give your repository a name say, "testing-inventyv" in the repository name input field. Check "Add a README file". And then create the repository clicking the "Create Repository" button at the bottom of the the page.

![](https://i.imgur.com/4E7h196.png)

This will redirect you to your new repository on GitHub. To get ready to copy (clone) this repository onto your local machine, click the green “Code” button. Then select the **HTTPS** option, and copy the url below it.
> Note: Make sure you are selecting the **HTTPS** tab and **not** the SSH one.

![](https://i.imgur.com/ZIp9vo6.png)

Once copied, open up the terminal where you wish to put this repo, and then add `git clone` before the url,
```bash
git clone https://github.com/amanverasia/testing-inventyv.git
```

Replace the link in the above command with your own.
![](https://i.imgur.com/pDgOv2T.png)

That is it! You created a repo and successfully connected it with your Git Client offline. You can open the folder and double check the url that you have imported the repo from by using,

```bash
git remote -v
```

![](https://i.imgur.com/205ThPe.png)

#### Using the Git workflow
Now that we have figured out how to download and open repos that we have created, now it's time for us to use some basic commands and figure out how they work. Now for this, I shall be creating and editing some basic files, feel free to do your own thing and change the things.

Let's start,

1. Create a new file in the `testing-inventyv` folder called “hello_world.txt” with the command `touch hello_world.txt`.

2. Type `git status` in your terminal. In the output, notice that your hello_world.txt file is shown in red, which means that this file is not staged.
![](https://i.imgur.com/zAXgicK.png)

3. Type `git add hello_world.txt`. This command adds your hello_world.txt file to the staging area in Git. The staging area is part of the two-step process for making a commit in Git. Think of the staging area as a “waiting room” for your changes until you commit them. Now, type `git status` again. In the output, notice that your file is now shown in green, which means that this file is now in the staging area.
![](https://i.imgur.com/ngHAPgd.png)

4. Type `git commit -m "Add hello_world.txt"` and then type `git status` once more. The output should now say: “_nothing to commit, working tree clean_”, indicating your changes have been committed. Don’t worry if you get a message that says “_upstream is gone_”. This is normal and only shows when your cloned repository currently has no branches. It will be resolved once you have followed the rest of the steps in this project.
![](https://i.imgur.com/xZW8AWq.png)

5. Type `git log` and look at the output. You should see an entry for your “_Add hello_world.txt_” commit. You will also see details on the author who made the commit and the date and time of when the commit was made. If your terminal is stuck in a screen with (END) at the bottom, just press “q” to escape. You can configure settings for this later, but don’t worry about it too much for now.
![](https://i.imgur.com/GjcAMYo.png)

6. Now I can also modify a file by using `nano`. Let's do that in the terminal using, `nano hello_world.txt` and then writing whatever changes we want, and exiting the file using ***Crtl + X*** and typing ***Y*** when asked for confirmation. (You can just use your own favorite text editor if you are not comfortable with terminal based text editors)
![](https://i.imgur.com/RLjVHyP.png)

7. Once the changes are made, if you now type `git status` you will see that the *hello_world.txt* file has modified written next to it, as well as it is not staged. We can simply use the command `git add .` where the dot(.) just adds all the files in the current directory to the staging area, and then we can commit using our `git commit` command.
![](https://i.imgur.com/7fTUU8a.png)

Those were some of the basic commands that are used on a day-to-day basis when using Git.

#### Pushing the Repo
Now working on the local Git client is helping us keeping a history of our code, we can even look at the commit history and all the logs, but it is very limiting in our experience because we are missing out on the collaboration part of GitHub. So an integral feature is to push our changes to our repo that we created on GitHub. 

Remember, that we were just making changes to the repository locally after we cloned it (downloaded it). Now we need to sync those changes. The command for that is `git push`. The actual command is, `git push origin main` but since we are not dealing with multiple branches (we will do that in a while) at the moment, so `git push` will do just fine.

```bash
git push
```

Now if you configured it properly in one of the previous steps i.e. [[#Step 4 Adding Token to Git]]. Then it should show something similar to the below given screenshot. If the command is throwing an error or asking for authentication, that means something went wrong with the authentication token, and you might want to set it up again.
![](https://i.imgur.com/56etKqr.png)

Now if we check out web browser by visiting our repository online on GitHub, we will see that our new files are right there, and we can even see our commit messages. Check the screenshot below for highlighted points of interests.
![](https://i.imgur.com/fijfs2U.png)

Here in the online interface, we can see our past commits, when we click on the *commits* count, as shown below in the screenshot.

![](https://i.imgur.com/tUKdIqT.png)

## Ending Thoughts

That concludes the documentation for GitHub basics training. The documentation can be used as a reference by yourself and contains enough notes and extra reading material for you to dive deep into the concepts if you wish to. Getting a mastery in these topics is not a difficult task and can be achieved through more and more practice. Consider spending some time with these commands and experimenting more with them if and when required.
