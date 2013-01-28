# Git Extensions

A collection of bash scripts to help with day to day use of Git created by [Dan Lister](http://github.com/danlister). Loosely based on and inspired by [Git Flow](http://github.com/nvie/gitflow). It was created to help maintain consistent commit messages and release procedures. Consistent messages within repository scripts are used to help with service hook integration to [Pivotal Tracker](http://www.pivotaltracker.com/).

## Service Hooks

In order to take advantage of commit references within commit messages and amending Pivotal Tracker story states, you will need to setup up a service hook between your Git repository and Pivotal Tracker account. Take a look at Dan Podsedly's [blog post](http://pivotallabs.com/users/dan/blog/articles/1304-github-service-hook-for-pivotal-tracker) for more information on how to setup service hooks for Pivotal Tracker and GitHub.
	
## Usage

### gitcommit

The commit script performs a commit. It outputs a commit message which could integrate with Pivotal Tracker if service hooks are setup. A comment on the story specified will be left, referencing the commit. The Pivotal Tracker story will be started if not yet started. The commmit script will only commit staged files.
	
	gitcommit <story-id> "<commit-msg>"

### gitdeliver

The deliver script performs a commit. It outputs a commit message which could integrate with Pivotal Tracker if service hooks are setup. A comment on the story specified will be left, referencing the commit and stating that the commit delivered the story. The deliver script will only commit staged files.
	
	gitdeliver <story-id> "<commit-msg>"

### gitfix
	
The fix script performs a commit. It outputs a commit message which could integrate with Pivotal Tracker if service hooks are setup. A comment on the story specified will be left, referencing the commit and stating that the commit fixed the story. The Pivotal Tracker story will be finished if not yet started or finished. The fix script will only commit staged files.

	gitfix <story-id> "<commit-msg>"

### gitstage

The stage script provides an easy and consistent way of releasing a development version to stage. While present on a development branch, we can specify the version being released. If already released, an error will occur. If not, the script will checkout to the staging branch and fetch the latest from it's origin. A merge of the development branch will be performed into the staging branch. If the merge fails, the script will die. If completed, a tag will be created stating the version being release. Both the staging branch and tag will be pushed to the repositories origin. The script then checks back out to your development branch, ready for you to continue working on your next version. Please note that each version number needs to be unique and not already present as a tag.

	gitstage <version>

### gitrelease

The release script performs a release of a tagged version to the master branch. This can be run from any branch, normally dev. The script will checkout the master branch, pull down the latest from origin and create a temporary branch for merging back into master based on the commit reference the version tag holds. Once merged, the temporary branch used for merging is removed. The temporary branch is never pushed to origin. The script, once finished, will always checkout to the dev branch once completed.

	gitrelease <version>
