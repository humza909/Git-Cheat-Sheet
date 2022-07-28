## Git Cheat Sheet
Various git commands at one place that we use regularly in our working life.
## Table of Contents
1. [Basic Git Commands](#basic-git-commands) <br />
2. [Working with Submodules](#working-with-submodules) <br />
3. [Working with Forks](#working-with-forks) <br />
#### Basic Git Commands:
<pre><code>git status  # new updates in repo
git add &lt;file-name> # add new files to commit
git commit -m 'your-message' 
git push  # push to remote 
git pull  # pull from remote
git log   # commits log
git reflog  # tracks local Git refs along with remote
git clone &lt;url> 
git checkout -b &lt;branch>
git branch -d &lt;branch_name>  # delete local branch 
git branch -D &lt;branch_name>  # forced delete local branch
git reset --hard HEAD~1  # removes your top commit if your head points there
git reset --soft HEAD~1  # in case if you want to get your work back
git remote remove origin  # remove remote origin 
</code></pre>

Clone submodules and a branch at a given depth (depth=1, clone's a large branch quickly 
with latest code):
<pre><code>git clone &lt;url> --recurse-submodules --depth=&lt;depth> -b &lt;branch>
</code></pre>

Pull a large repo quickly if cloned with depth=1. If new commits are merge-commits try pull with a larger 
depth may be 10 : 
<pre><code>git pull --depth=10 </code></pre>

To retrieve all:
<pre><code>git pull --unshallow </code></pre>

Know your repo's remote info:
<pre><code>git remote -v  # repo's remote url
git branch -va  # repo's available remote branches</code></pre>

Update repo's remote url. In case your repo is moved 
to some other url:
<pre><code>git remote set-url origin &lt;remote-repo-url-here> </code></pre>

Cache git credentials:
<pre><code>git config --global credential.helper "cache --timeout=&lt;time in seconds>" </code></pre>

#### Working with Submodules
Basic submodule commands
<pre><code>git submodule add &lt;url>  # add a submodule in repo
git submodule init  # initialize submodules
git submodule update  # updates submodules
git submodule update --init  # initialize and update submdoules
git submodule update --init --recursive  # to intialize, fetch and checkout nested submodules
git submodule update --remote --merge  # merge remote changes locally
git submodule update --remote --rebase  # reabase local with remote changes
git submodule foreach git pull origin &lt;branch>  # pull updates from all submodules
</code></pre>


Push submodule changes
<pre><code>git submodule foreach git push -u origin &lt;branch> 

# Or add submodule path manually
git add &lt;submodule-changes>
git commit -m ''
git push
</code></pre>

Update submodule's remote url. In case moved to some
other url:
<pre><code># new url local submodule is pointing to:
git config --file=.gitmodules submodule.&lt;submodule-path-in-file-here>.url &lt;url> 

# new branch local submodule is pointing to:
git config --file=.gitmodules submodule.&lt;submodule-path-in-file-here>.branch &lt;branch>

# After updating, run following to update submodules:
git submodule sync
git submodule update --init --recursive --remote
</code></pre>

#### Working with Forks
Clone your fork and do the following as required: 
<pre><code>git remote -v  # shows your fork remote
</code></pre>

To synchronize your fork with main repo:
<pre><code>git add upstream &lt;url>  # your main repo url, now above command will show both remote urls
git fetch upstream  # fetches all the branches
git fetch upstream &lt;branch> --depth=&lt;depth>  # to fetch specific branch at the given depth

# In case if u fail to fetch run this and then fetch again:
git config --local --add remote.origin.fetch +refs/heads/*:refs/remotes/origin/*

git branch -va  # to see remote and local branches

# Checkout a fork-branch and run merge commands mentioned below in this section to sync
# your branch
git checkout &lt;branch>  
</code></pre>

 To create a new local branch from upstream dev because fork and original repo could have 
 same names, if not done this way git will create a temporary branch itself with a
 detached head. Dev branch name is an example:
<pre><code>git checkout -b upstream-dev upstream/dev  # creates a local branch upstream-dev 

# And to push from a local branch to upstream, add commit and push by:
git push -u upstream &lt;branch>
</code></pre>

In order to merge an upstream branch with fork branch:
<pre><code>git fetch upstream master  # upstream branch
git checkout dev  # fork branch 
git merge master  # will merge master in dev 
</code></pre>

#### Contirbution
PRs are welcome from the community
