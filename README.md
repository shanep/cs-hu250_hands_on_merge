# cs-hu250_hands_on_merge

This assignment will familiarize you with git merge conflicts and their resolutions using a 3-way-merge. 
The major steps in this assignment are:

1. adding a new branch with one commit
2. adding a commit to master that modifies the same portion of of a file that was modified in the branch
3. merging the branch into master resulting in a conflict
4. resolving the merge conflict using a 3-way-merge

## Prerequisites
Setup vimdiff as your mergetool. If you want to use a GUI program you are free to use P4Merge or something similar.

    $ git config --global merge.tool vimdiff

## Step 1

Create a file called Main.java containing the code:

```
public class Main
{
    //this is the chronological revision 1 in master
    public static void main(String[] args)
    {        
        System.out.println("Hello world");
    }
}
```

Commit the changes as "revision one (in master)"


## Step 2

Create a branch called branch-feature and switch to it.

Edit the following code in the Main.java file in the branch:

```
public class Main
{
    //this is the chronological revision 2 in branch-feature
    public static void main(String[] args)
    {
        System.out.println("Hello world");    
     }
    public void methodInBranch()
    {
        System.out.println("Method in branch");
    }
}
```

Commit the changes as "revision two (in branch-feature)"

## Step 3

Switch to the master branch and edit the following code in `Main.java`:

```
public class Main
{
    //this is the chronological revision 3 in master
    public static void main(String[] args)
    {
        System.out.println("Hello world");
    }
    public void methodInMaster()
    {
        System.out.println("Method in master");
    }
}
```

Commit the changes as "revision three (in master)"

## Step 4

While still in the master branch, merge the branch branch-feature in master using:

  $ git merge branch-feature

The previous command should result in a merge conflict.

## Step 5

Start the 3-way-merge tool using:

  $ git mergetool

If the merge tool is configured correctly, this command should display the merge conflict in vimdiff

## Step 6

Resolve the conflict by including in the final (resolved) version of Main.java:

- only the latest change to the comment before the `main` method (i.e., "`//this is the chronological revision 3 in master`")
- both the `methodInBranch()` from `branch-feature` (Step 2) and the `methodInMaster()` from `master` (Step 3) branches.


### Step 6.1
Save the changes in vimdiff and close it.

  To exit vimdiff type <esc> :wqa 


## Step 7

In the git bash console, issue a git status to find out the appropriate Git command for finalizing the merge conflict.


### Step 7.1

The previous git status command might reveal some `*.orig` files generated during the merge conflict that can be removed manually:

```
$ rm *.orig
```

(Optional) Git can be configured to not create these `*.orig` files during future merge conflicts:

  $ git config --global mergetool.keepBackup false


## Step 8

Finalize the merge of the branch-feature into master, by running the git command discovered in Step 7, which should result in the creation of a new (merge) commit (e.g., "`Merge branch 'branch-feature'`").
