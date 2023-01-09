# Development-Guide-Lines

**Version Control**

All repositories use `Git` and are hosted on either `GitHub` or `CodeCommit` or `Git Lab`.

**Repository Naming**

If a repository contains the source code of the a site, its name should be the main naked domain name of that site. It should be lowercased:

Good: `pei.com`

Bad: `www.pei.com`, `https://pei.com`

Sites hosted on a subdomain may include the subdomain:

Good: `dev.pei.com`

Bad: `pei.com-dev`

If the repository concerns something else, for example a cron script, its name should be descriptive and must be kebab-cased.

Good: `cron-salesforce-transaction-sync`

Bad: `SalesforceTransactionSync`

**Branches**

Once a project has gone live, the `master` or `main` branch must always be stable. It should be safe to deploy the `master` branch to production at all times. All branches are assumed to be active; stale branches should get cleaned up accordingly.

Avoid committing directly to `master`. Updates should never be merged to `master` by anyone except the project’s lead developer.

**Repositories in Development**

All code bases that are in progress will have at least two branches: `master` and develop. Avoid commiting to `master`, always commit to develop. Feature branches should be branched from develop. Commits may be made directly to develop, though feature branches are strongly encouraged.

Once the project is ready for production, the develop branch will be dropped.

**Repositories in Production**

All commits to `master` must be made through feature branches.

**Naming**

There's no strict ruling on feature branch names. Branch names must be clear enough to know what

they're for and must be kebab-cased.

Good: feature-mailchimp, fix-deliverycosts or issue-sage-2766

Bad: feature/mailchimp-integration, random-things, develop

**Work in Progress**

All work in progress must be pushed to the remote repository frequently as no code should live solely on an individual contributor’s local machine. **At an absolute minimum all code must be pushed at the end of each working day**. This ensures that works in progress are available to the entire team should you need help with a complex problem, have a question about how to organize or structure something, or are out of office and another member needs to reference the code being written. Additionally it ensures that a backup of your work exists in case your computer crashes, your files get deleted, or your local machine is otherwise unavailable.

**Commits**

Commits must be granular and descriptive commit messages are required. A commit message with less than 3 words is likely an indication that the message is not descriptive while a message longer than 10 words may indicate that commits are not granular enough.

Descriptive: Update dependencies, Fix vat calculation in delivery costs

Non-descriptive: wip, commit, a lot, solid

Granular commit messages:

Acceptable: `Cart fix`

Better: `Fix add to cart button`, `Fix cart count on home`

Guides to creating better commits:

[The Art of the Commit by David Demaree](https://alistapart.com/article/the-art-of-the-commit/)

[Commit Message Driven Development by Andrew Feeney](https://andrewfeeney.me/articles/commit-message-driven-development)

[Preemptive commit comments by Arialdo Martini](https://arialdomartini.wordpress.com/2012/09/03/pre-emptive-commit-comments/)

[A Beginner’s Guide to Git — How to Write a Good Commit Message by Gaël Thomas](https://www.freecodecamp.org/news/a-beginners-guide-to-git-how-to-write-a-good-commit-message/)

[How to Write Good Commit Messages: A Practical Git Guide by Bolaji Ayodeji](https://www.freecodecamp.org/news/writing-good-commit-messages-a-practical-guide/)

**Creating Granular Commits**

If you've made multiple changes but want to split them into more granular commits, use `git add -p`. This will open an interactive session in which you can choose which chunks you want to stage for your commit.

**
Pull Requests**

In order to merge code to be deployed to staging or production a pull request must be created and submitted for review. All code must be reviewed by the project’s lead developer.

**Merging and Rebasing**

To avoid merge conflicts, your feature branch should be kept up to date by rebasing regularly. In order to keep default branches clean, use --squash when merging to `master` or `develop`:


`$ git merge <branch> --squash`
	
To learn more about the difference between merging and rebasing, see:

- [Merging vs. Rebasing on Atlassain](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)

- [Getting solid at Git rebase vs. merge by Christophe Porteneuve](https://medium.com/@porteneuve/getting-solid-at-git-rebase-vs-merge-4fa1a48c53aa)

Note that `--squash` does not create a merge commit automatically and that you’ll need to run `git commit` afterward. If you are content with the default commit message (a consolidation of all squashed commit messages) the following may be used:


`$ git merge <branch> --squash && git commit --no-edit`
	
**Naming and Messages**
	
Pull request titles should describe the feature being merged. Messages should describe the feature and list any closed tickets associated with the pull request.

**Included Files**
	
Only source files should be included in a Git repository. Dependencies, user uploaded assets, and IDE configurations, log files, caches, and similar files should be omitted. The following is an example of files that could be added to a `.gitignore` and is by no means meant to be exhaustive.

**Cache and Log Files**
	
```
/**/.*cache*/
/tests/_output
*.log
.*.cache
```
	
**Database Dumps**
	
```
*.sql
*.sqlite
```
	
**Dependencies**
	
```
/**/node_modules*/
/vendor
composer.phar
npm-debug.log
yarn-error.log
```	
  
**Generated Files**
	
```
/public/robots.txt
/public/sitemap*.xml
```
	
**IDE Settings**
	
```
/.idea
/.vscode
/.vagrant
```
	
**OS Files**
	
```
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db
```
	
**Packages**
	
```
*.7z
*.dmg
*.gz
*.iso
*.jar
*.rar
*.tar
*.zip
*.box
*.phar
```
	
**Aliasing**
	
Similar to shell aliases, [Git provides a mechanism for creating aliases](https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases). This can be quite useful to create short commands or to create single commands out of multiple commands you find yourself repeating frequently. Below are some examples of useful aliases:

```
[alias]
	co = checkout
	cop = "! f(){ git checkout ${1}; git pull; }; f"
	cob = checkout -b
	coo = !git fetch && git checkout
	br = branch
	m = merge --ff
	squash = "! f(){ git merge ${1} --squash --ff; git commit --no-edit; }; f"
	st = status
	aa = add -A .
	cm = commit -m
	aacm = !git add -A . && git commit -m
	cp = cherry-pick
	amend = commit --amend -m
	`master` = !git checkout `master` && git pull origin 
	po = push origin
	pom = push origin `master`
	poh = push origin HEAD
	plo = pull origin
	plom = pull origin `master`
	ploh = pull origin HEAD
	unstage = reset --soft HEAD^
	ls = log --pretty=format:"%C(yellow)%h%Cred%d\\ %Creset%s%Cblue\\ [%cn]" --decorate
	ll = log --pretty=format:"%C(yellow)%h%Cred%d\\ %Creset%s%Cblue\\ [%cn]" --decorate --numstat
	set-origin = !git push --set-upstream origin $(git rev-parse --abbrev-ref HEAD)
	ignore = update-index --assume-unchanged 
	follow = update-index --no-assume-unchanged
	edit-config = config --global --edit
```	
