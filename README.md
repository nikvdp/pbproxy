# pbproxy - send your clipboard anywhere you can ssh

**TL;DR:** `pbcopy` and `pbpaste` from any (mac or linux) machine you can ssh to

This is a simple tool to make it easy to interact with clipboards on remote
machines. The "ui" mimics macOS's `pbcopy` and `pbpaste` commands using the
original `pbcopy` and `pbpaste` on macOS, and wrapping `xsel` on Linux boxes.
On linux boxes where xsel is not available (eg headless servers that don't have
X) it falls back to storing clipboard contents in a temp file

In other words, you can `pbcopy` and `pbpaste` from any remote machines you
have ssh access to. The special sauce is that you can put a server name from
your ssh config on the end of a pbcopy or pbpaste command so you can do stuff
like run `echo hello | pbcopy server2` on server1, after which doing `pbpaste`
from server2 would print 'hello'. You can also do this in the other direction
with pbpaste, eg from server2 you can run `pbpaste server1` and it'll print out
the contents of server1's clipboard.

## Usage:


- Print the contents of another machine's clipboard to your local machine's stdout:
  ```
  pbpaste <some-server>
  ```
- Insert data into another machine's clipboard: 

  ```
  echo hello there | pbcopy <some-server>
  ```

  You can also use this to send the contents of your current machine's
  clipboard to another machine: 

  ```
  pbpaste | pbcopy <some-server>
  ```

- Print the contents of your local clipboard to stdout: `pbpaste`
- Insert data into your local clipboard: `echo some data | pbcopy`

**NOTE**: This tool works the same way regardless of if it's running on a macOS or
linux machine, on macs it wraps the native pbcopy and pbaste commands, and on
linux it uses xsel or a temp file
  

## Installation

- Clone this repo to your local machine
- Add the folder you cloned it to to your `PATH` through your
  `~/.bashrc`/`~/.zshrc` files (**NOTE**: on macOS, make sure it comes BEFORE
  `/usr/bin` on your PATH, otherwise the native `pbcopy` and `pbpaste` will
  take precedence)
- restart your shell (or on zsh do `hash -r`) and try it out.

