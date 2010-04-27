!SLIDE smbullets incremental
# collaboraton

!SLIDE center smbullets incremental
# discussing 2 types
### ad hoc & standard
* (i just made those up)

!SLIDE smbullets incremental
# both revolve around 'remotes'
## ...we'll cover those in a minute

!SLIDE smbullets incremental
# ad hoc
* local network
* requires web server on sharing machines
* (think 'hacking at conferences')
* (or [#bscamp](http://groups.google.com/group/bscamp/))

!SLIDE smbullets incremental
# standard
## something like [github](http://github.com)
## or [gitosis](http://github.com/res0nat0r/gitosis)
* (sidenote: [here's](http://scie.nti.st/2007/11/14/hosting-git-repositories-the-easy-and-secure-way) an old gitosis setup tutorial I've used)

!SLIDE
# both revolve around remotes
### so, what are they?

!SLIDE smbullets incremental
# remotes
* repositories on other machines
* with names
* (so you don't have to remember the uri)

!SLIDE smbullets incremental
# adding remotes
* git remote add toms git@github.com:tomkersten/bscamp-git.git
* 'toms' now refers to my repository on github

!SLIDE smbullets incremental
# getting my changes
* $ git fetch toms
* $ git [merge/rebase] toms/master
