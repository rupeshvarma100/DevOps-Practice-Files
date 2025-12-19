
Task 1 :    
    A couple of new Git repositories were created recently and this is still in progress. The developers now has started adding some content under these repositories. Below are the details for this request. 

    There is a file named lion-and-mouse-t1q5.txt which is placed under /home/sarah/story-blog-t1q5 repository, stage the same to make it available for commit.

    Use below credentials to SSH into the storage server and to complete this task.

Username: sarah
Password: S3cure321

Solution : 
    cd /home/sarah/story-blog-t1q5
    ls -la lion-and-mouse-t1q5.txt  # Confirm file exists
    git status  # Check current status (should show untracked)
    git add lion-and-mouse-t1q5.txt  # Stage the specific file
    git status  # Verify: file now under "Changes to be committed"



Task 2:
    A developer was in the process of creating repositories on the Gitea server. Unfortunately, one repository was mistakenly created and now needs to be deleted. Below are further details regarding this issue.


    The repository name is story-blog-t1q1 and is located under the sarah user on the Gitea server. The Gitea login credentials are as follows:

    Username: sarah
    Password: S3cure321

Solution : 

    Log into the Gitea server as user sarah with password S3cure321, navigate to the story-blog-t1q1 repository under the sarah user, and delete it via the web UI Settings in the Dangerous Zone.​

    Access Gitea
    Open a web browser and go to your Gitea server's URL (typically http://gitea-server-ip:3000 or similar, check your lab environment). Log in using username sarah and password S3cure321.​

    Delete Repository Steps
    Click on the story-blog-t1q1 repository under sarah's repositories list.​

    Select Settings tab at the top.

    Scroll to Dangerous Zone section at the bottom.

    Click Delete this repository.

    Confirm by typing the exact repository name sarah/story-blog-t1q1 in the prompt.

    Click the final delete confirmation button.​

    The repository will be permanently removed; no recovery option exists, matching Gitea workflows similar to GitHub.​

Task 3:
    The developers are adding some content under new repositories. There was some data added under /home/sarah/story-blog-t1q8 repository on the storage server. Commit the files that are currently in the staging area under this repository.


    First check the status of the file using the command git status. Then commit using the commit message as Added the lion and mouse story

    Use below credentials to SSH into the storage server and to complete this task.

    Username: sarah
    Password: S3cure321

Solution :

    SSH into the storage server as sarah with password S3cure321, navigate to /home/sarah/story-blog-t1q8, check staged files with git status, and commit using the specified message.​

    Access and Check Status
    
    ssh sarah@storage-server-ip  # Use actual storage server IP from lab

    cd /home/sarah/story-blog-t1q8

    git status  # Shows staged files under "Changes to be committed" *Commit Staged Files*
    
    git commit -m "Added the lion and mouse story"

Task 4:
    Nautilus developers are actively working on one of the project repositories, /usr/src/kodekloudrepos/apps-t2q1. Recently, they decided to implement some new features in the application, and they want to maintain those new changes in a separate branch. Below are the requirements that have been shared with the DevOps team:


    On Storage server in Stratos DC create a new branch xfusioncorp_apps-t2q1 from master branch in /usr/src/kodekloudrepos/apps-t2q1 git repo.

    Please do not try to make any changes in the code.

    Use below credentials to SSH into the storage server and to complete this task.

    Username: sarah
    Password: S3cure321


Task 5 :

    One of the Nautilus developers created some files under /home/sarah/story-blog-t1q10 repository on storage server, push these files to the remote git repository.

    Login info:

    Username: sarah

    Password: S3cure321

    remote repo alias : origin

    remote branch : master

Solution :
    Access Server
    From your jump host or local terminal, connect via SSH:

    text
    ssh sarah@ststor01.stratos.xfusioncorp.com
    # Or use IP: ssh sarah@172.16.238.15
    Enter password: S3cure321 when prompted. Accept host key on first connection.
    ​

    Verify and Stage Files
    Navigate and check repository status:

    text
    cd /home/sarah/story-blog-t1q10
    git status
    ls -la  # Confirm new files from Nautilus developer
    git add .  # Stage all new/changed files (or git add <specific-file>)
    git status  # Verify files under "Changes to be committed"
    Fix ownership if permission denied: sudo chown -R sarah:sarah /home/sarah/story-blog-t1q10.
    ​

    Commit Changes
    Create a commit with descriptive message:

    text
    git commit -m "Add new files from Nautilus developer"
    git log --oneline -3  # Verify latest commit
    This records changes locally before pushing.
    ​

    Push to Remote
    Push to the specified remote and branch:

    text
    git remote -v  # Confirm origin points to correct remote repo
    git push origin master
    The -u flag can set upstream tracking: git push -u origin master. Verify with git status (should show "up to date").
  
    ​
Task 6:

    A couple of new Git repositories were created recently and this is still in progress. The developers now has started adding some content under these repositories. Below are the details for this request.


    There is a file named lion-and-mouse-t1q5.txt which is placed under /home/sarah/story-blog-t1q5 repository, stage the same to make it available for commit.

    Use below credentials to SSH into the storage server and to complete this task.

    Username: sarah
    Password: S3cure321

Solution : 

    Connect to Server
    Use SSH from your jump host or terminal:

    text
    ssh sarah@ststor01.stratos.xfusioncorp.com
    # Password: S3cure321
    This accesses the Stratos DC storage server where repositories reside.
    ​

    Navigate Repository
    Change to the target directory and verify file:

    text
    cd /home/sarah/story-blog-t1q5
    ls -la lion-and-mouse-t1q5.txt  # Confirms file exists
    git status  # Shows untracked/modified files
    Ownership fix if needed: sudo chown -R sarah:sarah /home/sarah/story-blog-t1q5.​

    Stage the File
    Add the specific file to staging area:

    text
    git add lion-and-mouse-t1q5.txt
    git status  # Verify under "Changes to be committed"



Task 6:

    Sarah created a new file named notes-t1q9.txt under /home/sarah/story-blog-t1q9 repository where she plans to write down ideas about the story for personal purposes. She does not want git to track this file or share it with her team mates.

    It is good that the file is untracked. But it is still under GIT's radar. If you run the git add . command, accidentally git will start to track this file.


    Let's configure git to ignore this file permanently.

    Use below credentials to SSH into the storage server and to complete this task.

    Username: sarah
    Password: S3cure321

Solution:

    Connect to Server
    Access the Nautilus storage server:

    text
    ssh sarah@ststor01.stratos.xfusioncorp.com
    # Password: S3cure321
    This connects to the Stratos DC environment hosting the story-blog repositories.
    ​

    Navigate Repository
    Change to the target directory and verify setup:

    text
    cd /home/sarah/story-blog-t1q9
    ls -la notes-t1q9.txt  # Confirm file exists and is untracked
    git status  # Should show notes-t1q9.txt as untracked
    Fix permissions if needed: sudo chown -R sarah:sarah /home/sarah/story-blog-t1q9.​

    Configure Git Ignore
    Create or edit .gitignore to permanently ignore the file:

    text
    echo "notes-t1q9.txt" >> .gitignore
    # Or use: echo notes-t1q9.txt > .gitignore (creates new if missing)
    git add .gitignore
    git commit -m "Ignore personal notes-t1q9.txt file"
    Verify with git status - notes-t1q9.txt no longer appears even after git add ..

Task 7:

    Connect to Server
    Access the Stratos DC storage server:

    text
    ssh sarah@ststor01.stratos.xfusioncorp.com
    # Password: S3cure321
    Navigate to the cloned repository: cd /usr/src/kodekloudrepos/demo-t2q3.
    ​

    Create Branch and Copy File
    Ensure on master and create new branch:

    text
    git checkout master
    git pull origin master  # Ensure latest
    git checkout -b nautilus-t2q3
    cp /tmp/index-t2q3.html .
    git add index-t2q3.html
    git commit -m "Add index-t2q3.html from /tmp"
    Verify: git status shows clean working tree.
    ​

    Merge and Push Changes
    Switch back to master, merge, and push both:

    text
    git checkout master
    git merge nautilus-t2q3  # Fast-forward or create merge commit
    git push origin master
    git push origin nautilus-t2q3
    Confirm remotes: git remote -v (should show origin). Final git status shows up-to-date on master.
    ​

    Verify Completion
    Check branches and log:

    text
    git branch -a  # Lists local/remote branches
    git log --oneline -5  # Shows recent commits with index-t2q3.html
    Fix permissions if needed: sudo chown -R sarah:sarah /usr/src/kodekloudrepos/demo-t2q3.

Task 8:

    A new repository named /usr/src/kodekloudrepos/demo-t2q5 was created recently and some data was added in it. Now one of the developers wanted to use this repository further to add/update some data.


    Checkout the master branch under repo /usr/src/kodekloudrepos/demo-t2q5.

    Use below credentials to SSH into the storage server and to complete this task.

    Username: sarah
    Password: S3cure321

Solution :
    Connect to Server
    Access the Stratos DC storage server:

    text
    ssh sarah@ststor01.stratos.xfusioncorp.com
    # Password: S3cure321
    This connects to the Nautilus environment hosting kodekloudrepos.
    ​

    Navigate and Checkout Master
    Change to the repository and switch to master branch:

    text
    cd /usr/src/kodekloudrepos/demo-t2q5
    git checkout master
    git status  # Confirms "On branch master"
    Updates local master with latest remote changes if needed: git pull origin master.
    ​

    Verify Status
    Check current branch and repository state:

    text
    git branch  # Shows * master (current branch)
    git log --oneline -3  # Recent commits on master
    Fix permissions if access denied: sudo chown -R sarah:sarah /usr/src/kodekloudrepos/demo-t2q5.​
    ​

