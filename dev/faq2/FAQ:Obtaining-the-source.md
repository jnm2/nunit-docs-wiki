Here are the steps you'll be following to set up your local system for working on NUnit code:

1. Fork the NUnit Repository on github
   click the fork button in the upper right corner
2. Clone from your NUnit fork
   $ git clone https://github.com/username/nunitlite.git
3. Create a working branch in your local repository for the feature / bug fix
   $ git branch <name_of_your_new_branch>
   $ git push origin <name_of_your_new_branch>
4. Checkout your work branch
   $ git checkout <name_of_your_new_branch>
5. Do your work on the branch, committing locally as you go
   $ git add <modified_file_name>
   $ git commit -m "<Commit Message>"
6. Push your changes to your fork on github
   $ git push origin <branch_name>
7. Make a pull request
   Switch to your branch
   [[https://github-images.s3.amazonaws.com/help/pick-your-branch.png]]

   Click the Start a review button
   [[https://github-images.s3.amazonaws.com/help/pull-request-start-review-button.png]]
8. Remove the local feature / bug branch
   $ git branch -d <name_of_your_new_branch>
9. Remove the remote feature / bug branch   
   $ git branch :<name_of_your_new_branch>