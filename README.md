PairUp!
=======

PairUp! is a Pair Programming Station that runs as a Stackato Application.

This stackato app will create a pairing programming environment that is clean
and repeatable and quick-n-easy to setup.

Initial Setup
-------------

You'll need admin access to a Stackato (1.2 or higher) VM.  You can install
your own with this command:

    curl get.stackato.com/microcloud | bash

Using the stackato command line client, run these commands:

    git clone git://github.com/ingydotnet/pairup.git
    cd pairup
    stackato target api.your.stackato.vm.domain
    stackato register yourself@example.com
    stackato register yourpair@example.com
    stackato login yourself@example.com
    stackato groups create pair
    stackato groups add-user pair yourself@example.com
    stackato groups add-user pair yourpair@example.com
    stackato group pair
    stackato push -n
    stackato ssh pairup

Now you are inside the pairing container. Run these commands:

    git clone your-pairing-repo-url conf
    pair setup

At this point, yourpair will need to download the [Stackato client](http://www.activestate.com/stackato/download_client), then run:
    
    stackato target api.your.stackato.vm.domain
    stackato login yourpair@example.com
    stackato group pair

Running
-------

After the above prep, both you and your pair will do the following:

    stackato ssh pairup

Then from within the VM:

    pair start

Whoever is the first to do it creates a `tmux` session (which has screen-like
bindings, e.g., it uses Ctrl+a instead of tmux's default Ctrl+b), and the
second one will do a `tmux attach`.

... need more doc here. stuff below is older ...

Future Ideas
------------

- Keep decent logs. E.g., prompt the users at the end of the session for a
  string describing what went on, then maybe snapshot the shell history plus
  any git commits into a single place for later reference.

- Socialize. For example, you could make a Kibitz Mode that announces the
  session (on Twitter, IRC, etc.), then netizens worldwide can log into
  wemux's readonly "Mirror" mode, then their comments appear in a sub-window.
  Should be easy to privilege them as read-write mode to invite them to drive.
  Could go nuts with this angle - for example, a company could sponsor a
  hackathon where there are tasks to grab, and you pair up do-si-do style with
  whoever might be available... maybe even have a contest aspect to it (such
  as winning points per task - or taking an existing codebase and trying to
  get as many "-" diffs as possible in refactoring.)

- Transportable sessions. E.g., you've got some good project going on,
  everything is set up, then you decide it would be smart to check it out on a
  machine that has a Windows VM. Instead of scratching your head figuring out
  how to install one, you zap the pair session over to some other host that
  already has one set up. In fact, I wonder if there's anything in the
  licenses that would prevent these hosts from being completely communal -- if
  not, you could make a slew of sandboxes ready to go -- everything from
  Windows 95 to 8, OSX Lion/Sabrecat/Meowbot3000, even maybe toss in some
  badly-configured ones, like filled with browser toolbars and spyware.

- Really good I/O with other machines - Of course pre-installed
  `gist`/`wgetpaste` CLI stuff, but also a way to get `xclip`/`xsel` talking
  with the host machine, perhaps add init prompts to do the `.ssh/id\_rsa.pub`
  exchange so that `scp` is quick both ways.

- Automate process of:
    - Creating Stackato user for pair guy
    - email/github/irc/twitter? invites

- Add mosh (MObile SHell)

Things to Check
---------------

- Why does the stackato group show up as 1034 in /app/fs/home/
