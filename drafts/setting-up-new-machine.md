As timing would have it, my laptop is having some deep troubles. Right before I start traveling for my sabbatical. Here's me trying to have a reasonably portable setup:

<!-- TEASER_END -->

There are two goals

1. Have everything live in the cloud so it can be restored as needed.
2. Get rid of things I don't really need.

# Step Zero

Back everything up to TimeMachine.

# Have everything live in the cloud so it can be restored as needed

I end up using Dropbox (personal, collaborations), Box (Earlham-only work), Google Drive (not as heavily used), and iCloud (pictures).


## Config files

I have a Dropbox folder called `dotfiles` that includes `.emacs.d` `.oh-my-zsh` `.zshrc` `.emacs` (all of which get linked from my homedirectory) and sshconfig, which gets copied to new machines.


## Code I work on

I keep all of this in `~/coding`. Many of these are git repositories, so this gets me most of the way:

```bash
for d in *
do
    echo $d
    cd $d
    git status
    cd ..
    echo "..."
done
```

For what it's worth, the `.git/config` in my blog directory looked like

```
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
        ignorecase = true
        precomposeunicode = true
[remote "origin"]
        url = git@github.com:mglerner/mglerner.github.io.git
        fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
        remote = origin
        merge = refs/heads/master
[branch "src"]
        remote = origin
        merge = refs/heads/src
```

Other things are easily recoverable as I want them, but don't forget

* [Chodera's StatMech](https://github.com/jchodera/statmech-for-biochemists)
* The velocyto tutorials

Working with Rick at NIH, I made a specific ~/Projects directory. It should probably live in the coding directory. For now, though, it lives in the Dropbox Suitcase mentioned elsewhere.

Otherwise, github is awesome. Nikola saving all of my blog stuff automatically to github is awesome.

## Code I use

I also had a `src` directory that had things I just used in it. This has been dwindling over time, but I might want to go grab [emacs-for-python](https://github.com/gabrielelanaro/emacs-for-python) ... but that looks like it hasn't been touched in five years, so maybe I should re-evaluate my emacs + python setup.

## Other files

I'm making a Dropbox folder specific to this task called `_Suitcase_August_2019_Move` and adding my .ssh id files. This is probably a bad and lazy idea.

I'm also adding whatever's on my Desktop. I'm preferencing speed and ease over beauty here.

## Photos

These all live in iPhoto in the iCloud iNow.

# Get rid of things I don't really need

Done via the list below, and things not being included in said list.

This also included **gasp** closing all of my browser tabs. Which included making some lists of bookmarks in markdown files in various github repos.

## Software I'm going to want

| Software                | Notes |
|---------------|------|
| Anaconda Python Distribution | I'll want the base env untouched, a coding env for coding, and a blog env for nikola | 
| Aquamacs |   |
| Acrobat Pro  | installed by IT  |
| Box |   |
| Cura for Wanhao|   |
| Drobo Dashboard |   |
| Dropbox |   |
| Firefox |   |
| Keybase |   |
| Microsoft Office Suite | installed by IT  |
| MacTeX |   |
| Moom |   |
| Papers |   |
| PASCO Capstone |   |
| Signal |   |
| Skype |   |
| Slack |   |
| Spotify |   |
| VMD |   |
| Wolfram CDF Player |   |

The only one of these I'm worried about is Slack. I never really know how to reinstall it, because I have some weird combination of "magic links" and emails and accounts and passwords and who knows what. Maybe it will just magically work, but I took screenshots of my workspaces just in case. Good thing, because Slack started showing up as blank right afterwords. Did I mention the deep computer issues? Ugh.

# About to flip the switch

This all seems a bit too easy. So we'll see what goes deeply wrong.
