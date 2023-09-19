

# gitwatch

A bash script to watch a file or folder and commit changes to a git repo.  
This is a fork from [original gitwatch](https://github.com/gitwatch/gitwatch) with these modifications:  
* commit author is the logged in user
* commit message is the hostname by default
* default waiting time before commit is 60 seconds


### Install

```sh
git clone https://github.com/pmamico/gitwatch.git
cd gitwatch
sudo install -b gitwatch.sh /usr/local/bin/gitwatch
```

## Requirements

To run this script, you must have installed and globally available:

* `git` ([git/git](https://github.com/git/git) | [git-scm](http://www.git-scm.com))
* `inotifywait` (part of **[inotify-tools](https://github.com/rvoicilas/inotify-tools)**)



## Usage

`gitwatch.sh [-r <remote> [-b <branch>]] <file or directory to watch>`

It is expected that the watched file/directory are already in a git repository
(the script will not create a repository). If a folder is being watched, this
will be watched fully recursively; this also means that all files and
sub-folders added and removed from the directory will always be added and
removed in the next commit. The `.git` folder will be excluded from the
`inotifywait` call so changes to it will not cause unnecessary triggering of
the script.

If you have any large files in your repository that are changing frequently,
you might wish to ignore them with a `.gitignore` file.

### systemd


* Create dir if it does not exist and copy systemd service file with
  `mkdir -p "$HOME/.config/systemd/user" && cp gitwatch@.service $HOME/.config/systemd/user`
* Start and enable the service for a given path by running
  `systemctl --user --now enable gitwatch@$(systemd-escape "/my/gitrepo").service`
