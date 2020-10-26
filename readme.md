# Hej lol

# How to fork this repository and setup the game on your machine
1. Start by creating a directory on your local machine where all your github projects should be placed. In this example we will call the directory for github projects.
2. Navigate to the previously created directory using either the bash command cd or by locating it and opening a terminal in your current directory (Type cmd in address bar on windows / right click in your folder and select 'Open in Terminal' on OS x/linux).
3. On github, you must click the 'Fork' button on the top-right. This creates a copy of the repository on your own github, meaning no changes that you do will occur on my repository.
4. You must now added your competitors as collaborators to this project inorder for them to edit your version of the game. 
	<details><summary>Hint</summary>
	<ul>
		<li> Go to Github and find your repository, if you don't already have it</li>
		<li> Click on settings in the menu bar for your repository</li>
		<li> Go to manage access</li>
		<li> Click on Invite a collaborator, on find your friends with email, username or full name, if they have a github account.</li>
	</ul>
	</details>
4. Now it is time to clone the repository, you do this by finding the https clone link on github. **For my repository, it is https://github.com/lass7965/DM500TicTacToe, but for yours it will be different**
	```git
	git clone https://github.com/lass7965/DM500TicTacToe.git
	```
5. A folder has now been created in your current directory which contains the files from the cloned repository. To view the contents of your current directory in the terminal you can do 'ls' on linux/OS x and 'dir' on windows.
6. Doing 'ls' or 'dir' in the terminal you should be able to see a folder with the name "DM500TicTacToe". Navigate to this folder by doing the 'cd' command in the terminal.
	```bash
	cd DM500TicTacToe
	```
## How to play the same game
1. Pick a person and use that person's repository.
2. All players, except picked owner of this repository from step 1, must then locate the https clone link on github for this repository. Using this link the repository should be cloned into the **github projects** folder. **Please avoid cloning a repository inside a repository as that really gets messy, so please navigate back to your github project folder before cloning. You can navigate back to the parent folder by doing 'cd ..' in your terminal**
# How to play the game:
## Starting the first game out:
1. On the very first turn, you will have to decide which one of you starts.
2. If it is your turn do:
	```git
	git pull
	```
3. Open the .tex document using your favorite text editor, and pick a eligible spot.
4. Compile the .tex document and check that you are satisfied with the changes in the created pdf file:
	```git
	pdflatex TicTacToe.tex
	```
5. Compiling the latex document created 5 new files, which git does not know exists. We need to make git know that the pdf file exists. Do the following command to check which files has been changed and which are "untracked"
	```git
	git status
	```	
6. We only want to add the pdf file to git, the rest can remain untracked:
	```git
	git add TicTacToe.pdf
	```
7. Now we want to prepare sending our changes to the shared git repository, we do this using the commit command:
	```git
	git commit -m "I have now made the winning move, you lose!"
	```
	The '-m' defines that you wish to define a message to the changes you made. The -m is followed by the message, where you should describe the changes you made.
8. Finally you push the changes to the git repository, making it available for your competitors in our game, but usually only available to you fellow collaborators, which concludes your turn. 
	```git
	git push
	```
## When it is your turn:
1. You start out your turn by pulling the latests changes to the repository. Please note, that due to some write access security, having the PDF open in any program will prevent the following command:
	```git
	git pull
	```
2. Open the pdf, check that the player before you's move has been added, and check if that player has won. Should it not be added you need to go back and figure out what went wrong.
3. Open the .tex document using your favorite text editor, and pick an eligible spot.
4. Compile the .tex document and check that you are satisfied with the changes in the modified pdf file (**If you already had the pdf open, you might have to close it before compiling**):
	```git
	pdflatex tictactoe.tex
	```
5. Check that your move has correct in the pdf file.
5. Now we want to prepare sending our changes to the shared git repository, we do this using the commit command, but with a change from the previous 
	We replace -m with -am, and we do this as it is a contraction of -a and -m. -a is a special flag for the command that tells commit to prepare all **tracked modified** files for upload using the push command.
	```git
	git commit -am "Veni vidi vici"
	```
	Having two different commits with the same commit message is permitted in git, but we advise not doing to, as commit messages are used when having to go back to previous version of your code, should something break in later versions (Yes, it happens. Alot)
	
6. You finish you turn by pushing your changes to the git repository, which makes it available for the next players.
	```git
	git push
	```
## When a game ends:
1. The game ends when a person get 3 in a row.
2. Pick a person, could be the winner of the game but you should all try this.
3. In your terminal do the following and find the first move that all players made
	```git
	git log
	```
	Git log only shows you the logs for the past few commits, but more might be relevant. You can press enter reveal more commits.
	For leaving git log, you simply press q
4. The commit right before, should be a clean board with no moves made in the board, and you need to copy the commit ID. It looks something like this (0a790a68542e046fd2d05cb738ab819fb2107e9b)
5. We now wish to restore our files back to this clean board commit:
	```git
	git checkout 0a790a68542e046fd2d05cb738ab819fb2107e9b
	```
6. A new branch indicating a new game should then be created, as we want to keep the results from the first game.
	```git
	git switch -c game#2
	```
	Here the -c flag indicates that it should create a new branch locally if it does not exist.
7. A new branch has now been created locally and we now need to push this need branch to github.
	```git
	git push -u origin game#2
	```
8. You are now all set, but the other players are not, as they still are on the old game board. They should start out by doing:
	```git
	git pull
	```
9. By doing 'git branch' you are only able to see local branches, but we wish to see branches on the **r**emote host (Github). Therefore we do:
	```git
	git branch -r
	```
10. Locate the newly created branch and switch to this branch by replacing the branch name in the command below with '[Branch]'. **Please note that the origin/ should not be in the branch name when typed in the command below:**
	```git
	git switch [Branch]
	```
11. You are all now all set and you can start playing again!
# Handling merge conflicts:
1. Not all games are turn based, and neither is collaborating on github. Therefore something called a merge conflicts can occur. If you do not know or is unsure of what an merge conflict is, we recommend reading **Merge conflict explained** below.
2. The idea here is to cause a merge conflict to happen, and for setting stuff up you should do the steps in 'When a game ends' first.
3. You now have no idea of to who starts, therefore you all decide to be the one who starts. You should all therefore do
	```git
	git pull
	```
4. Open the .tex document using your favorite text editor, and eligible spot.
5. Compile the .tex document and check that you are satisfied with the changes in the modified pdf file (**If you already had the pdf open, you might have to close it before compiling**):
	```git
	pdflatex tictactoe.tex
	```
6. Check that your move has correct in the pdf file.
7. Commit your changes, remember to include the -am and remember to write an nice message!
8. In an order specified by you, you should all push your work to github.
9. The first push won't cause an error but the others will, and they will have to be solved!
10. As the push got rejected you have to **pull** the changes that was made
10. Open the .tex document using your favorite text editor, and locate the merge conflict.
	<details><summary>Hint</summary>
	It is marked by git with <<<<<<<< HEAD and <<<<<<<< [CommitID] and can occur at multiple in the code. 
	</details>
11. Delete one of the version (or keep both), most important is that you delete the <<<<<<<< HEAD and <<<<<<<< [CommitID]
12. Commit your changes, include -am and remember to write a message about your change and that a merge conflict occured but you fixed it.
13. Push your changes and go to step 3 until all have tried to handle a merge conflict.
## Merge conflict explained:
A merge conflict can occur when two or more changes are made by two or more persons, while working on the same base file. Imagine having a file with the following task written in it:
```java
public static void main(String[] args){
	//Make this function print the result of 2+2
}
```
Two different persons decides to do this task simultaneously, which causes them both to do the git pull command. They now both have the file with the unfinished task.
The first person is fast to do this function and quickly commit and push the following to github:
```java
public static void main(String[] args){
	//Make this function print the result of 2+2
	System.out.println("4");
}
```
The second person could be just a tiny bit slower to do the task. Therefore they commit and push their finished solution to the task after the first person, and they complete the task as follows:
```java
public static void main(String[] args){
	//Make this function print the result of 2+2
	System.out.println(2+2);
}
```
This second person would get a merge conflict as git does not know how to handle this as it does not know which of the codes are the most correct. Git knows that the second person is unaware of the changes made by the first person and thereby directly rejects the push, and instead advises the second person to fix the merge conflict.
