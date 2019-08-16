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

check all to make sure git up to date, make list. Make sure blog dir includes drafts?

## Code I use

## Other files

I'm making a Dropbox folder specific to this task called `_Suitcase_August_2019_Move` and adding my .ssh id files. This is probably a bad and lazy idea.

I'm also adding whatever's on my Desktop. I'm preferencing speed and ease over beauty here. 

# Get rid of things I don't really need

## Software I'm going to want

Aquamacs  
Acrobat Pro  [installed by IT]
Box
Cura for Wanhao  
Drobo Dashboard  
Dropbox
Firefox
Microsoft Office Suite  [installed by IT]
MacTeX
Moom
Papers
PASCO Capstone
Signal
Skype
Slack
Spotify
VMD
Wolfram CDF Player


## Software in question

Keybase

