Problem
-The Nautilus development team has initiated a new project development, establishing various Git repositories to manage each project's source code. Recently, a repository named /opt/demo.git was created. The team has provided a sample index.html file located on the jump host under the /tmp directory. This repository has been cloned to /usr/src/kodekloudrepos on the storage server in the Stratos DC.



Copy the sample index.html file from the jump host to the storage server placing it within the cloned repository at /usr/src/kodekloudrepos/demo.

Add and commit the file to the repository.

Push the changes to the master branch.




Solution Steps
1. Copy the file from jump host to storage server
scp /tmp/index.html natasha@ststor01:/usr/src/kodekloudrepos/apps/

Or if you're already on the storage server,
cp /tmp/index.html /usr/src/kodekloudrepos/apps/


2. Navigate to the repository
cd /usr/src/kodekloudrepos/apps

3. Verify the file exists
ls -l index.html

4. Add the file to Git
git add index.html

5. Commit the changes
git commit -m Add index.html file"

6. Push to master branch
git push origin master

What Went Wrong?
- You likely skipped Step 1 or copied the file to the wrong directory. Git can only track files that actually exist in the repository folder.