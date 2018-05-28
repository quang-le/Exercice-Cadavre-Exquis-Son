# **GUIDE GIT+GITHUB**

1. **Repo setup**

  * Create repo on https://github.com/quang-le?tab=repositories
  * Clone repo on desktop using provided link. **IMPORTANT**: do not create folder as `git clone` wil automatically create one
  * `cd /home/nb24/*newrepo*`
  * `touch README.md`
  * `gedit README.md` : fill in the file with useful info about the repo
  * `.gitignore` : use it to indicate which files GIT shouldn't follow **TO BE LEARNED**

2. **Normal flow**
  * `git pull`
  * Create your file locally
  * `git add *filename.ext*` or `git add .`(adds all folder contents)
  * `git commit -m "your comment"`
  * `git push origin *yourbranch*`

3. **Branching**
  * Create branch: `git branch *branchname*`
  * Move between branches `git checkout`
  * Create branch and move HEAD to new branch `git checkout -b *branchname*`
  * Push branch: `git push origin *branchname*`
  * Merge: merges the content of 2 branches: 
     * `git checkout *destination branch*`
     * `git merge *branchtomerge*`
  * Rebase: moves one branch onto another:
     * `git checkout *branchtorebase*`
     * `git rebase *destinationbranch*`

4. **Troubleshooting**

  * Merge conflict: `git commit -a`, then open file, make corrections, add, commit, push.
  * Rollback: **TO BE LEARNED BY 11/05**

5. **Misc**

  * Acces repos you've been invited to : Go to Github -> Right corner drop-down list (with profile) -> Settings
  * Move files from one repo to another without losing history **TO BE LEARNED**
