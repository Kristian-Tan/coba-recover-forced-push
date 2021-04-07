# coba-recover-forced-push

## About

My own experiment at doing tutorial found at: https://gist.github.com/agarwalparas/d355a950148702cc7ba82abc4d1943bf

## Credits

credit to agalwalparas for posting in gist, and credit to Sankara Rameswaran as (probably) the original author

## Content of the gist:

```
# First, you must get the previous commit sha, the one before the forced push:

## Hit through terminal
curl -u <username> https://api.github.com/repos/:owner/:repo/events

# Then you can create a branch from this sha:

## Hit through terminal
curl -u <github-username> -X POST -d '{"ref":"refs/heads/<new-branch-name>", "sha":"<sha-from-step-1>"}' https://api.github.com/repos/:owner/:repo/git/refs

#Finally, you can clone the repository locally, and force push again to master:
git clone repo@github
git checkout master
git reset --hard origin/<new-branch-name>
git push -f origin master

Credit: Sankara Rameswaran
```

## My scenario

This repo should contain this kind of history:

```
(initial_commit) <- (commit_1) <- (commit_2_bad) <- (commit_3) <- [master,head]
                               <- (commit_2_good)
```

commit `commit 2 good` will be replaced (by force push) with commit `commit 2 bad`

The goal here is to recover commit 2 good and make the history as follows:

```
(initial_commit) <- (commit_1) <- (commit_2_good) <- (commit_3) <- [master,head]
```

Each commit will create an empty file in root directory with it's commit name (except `initial_commit` which only creates README.md)

Steps on how it's done, what commands is run, and what are the outputs, will be written in wiki instead of in repository/source code
