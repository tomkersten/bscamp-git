!SLIDE
# merge vs. rebase

!SLIDE
# i rebase all the time
## unless i have to merge

!SLIDE
# which means i don't pull
### (that's not true, but i don't nearly as often as [roy](http://twitter.com/roykolak) does)

!SLIDE
# clean & clear commit logs
### are sexy to me

!SLIDE
# merges don't give you either

!SLIDE commandline
# merge
    $ git log
    commit 833328djkslj35f58edc2c8ef3f72e21659ae976
    Merge: c6ff987 5fc7389
    Author: Another Person <some_dude@somewhere.com>
    Date:   Thu Apr 22 14:20:15 2010 -0500

        Merge branch 'some_branch'

        * some_branch:
        Minor variable name change
        Removing duplication
        Corrected examples
        Updated this other thing
        Adding files

        Conflicts:
        spec/one_of_the_specs.rb

!SLIDE
# vs.

!SLIDE commandline
# normal
<br/>
<br/>
<br/>
    $ git log
    commit 63822392389sjdslsjkl54fa65b8a8a363a17e35
    Author: Some Person <someone@somedomain.com>
    Date:   Mon Jun 29 16:21:36 2009 -0400

        Fixing the coverage task for the current setup

!SLIDE
# merge
## is like a zipper

!SLIDE
![Zipper](zipper.jpg)

!SLIDE
# rebase
## is like a flux capacitor

!SLIDE
![Flux Capacitor](flux_capacitor.png)


!SLIDE
# that makes no sense
### unless you understand the fundamentals
### ...and you've seen ["Back to the Future"](http://www.imdb.com/title/tt0088763/)

!SLIDE
# there are 3 components
## in a git repository
### (basically)

!SLIDE
# you often see two of them
![Project Commit](github_commit.jpg)

!SLIDE
# blobs, trees, commits

!SLIDE
# blobs
## SHA1 hash of file size & contents
### same content == same blob == same file
### (to git)

!SLIDE
# example
### (you can follow along at home)

!SLIDE commandline incremental
    $ mkdir new_project
    $ cd new_project
    $ mkdir directory_1
    $ mkdir directory_2

    $ echo 'Content of README' > directory_1/README
    $ echo 'Content of README' > directory_2/README

    $ git hash-object directory_1/README
    d3f48b93b168b70f7bf91e27e6bbf0ef97d52821

    $ git hash-object directory_2/README
    d3f48b93b168b70f7bf91e27e6bbf0ef97d52821

    $ # [note: created git repository w/ a single commit]
    $ git cat-file blob d3f48b93
    Content of README

!SLIDE center
![SHA1 Computation](sha1s.png)

!SLIDE
# blobs
## takeaway: many files can have same blob sha1
### (that's important)


!SLIDE
# <span style="color: #777; text-decoration: line-through;">blobs,</span> trees, commits


!SLIDE
# trees
## think of them as directories
### (collection of multiple sub-nodes)

!SLIDE
# each commit has one
### composed of either sub-trees or blobs
### (id is collective sha1 of sub-nodes)

!SLIDE commandline incremental small
# in our example
    $ git ls-tree  HEAD
    040000 tree 10c195f4f039d79a0441fefb0e63e07d227edb89    directory_1
    040000 tree 10c195f4f039d79a0441fefb0e63e07d227edb89    directory_2
                ^^^^^^^^^^^^^^ SAME??! ^^^^^^^^^^^^^^^^^    ^^^ DIFFERENT?

    $ git ls-tree 10c195f4f039d79a0441fefb0e63e07d227edb89
    100644 blob d3f48b93b168b70f7bf91e27e6bbf0ef97d52821    README
           ^^^^

!SLIDE commandline incremental small
# quiz
    $ mkdir directory_3

    $ echo 'Content of README' > directory_3/different_file_name
                                             ^^^^^^ NOTE ^^^^^^^

    $ git add . && git commit -a -m"Added new file in directory_3"

    $ git ls-tree HEAD
    040000 tree 10c195f4f039d79a0441fefb0e63e07d227edb89    directory_1
    040000 tree 10c195f4f039d79a0441fefb0e63e07d227edb89    directory_2
    040000 tree 56b93cce25073a26c67c07d7fe0b744668bf0d32    directory_3
                ^^^^^^^^^^^^^^ DIFFERENT? ^^^^^^^^^^^^^^

                                  WHY?

!SLIDE commandline incremental small
# look at the trees
    $ # uhhh, check my flo'
    $ git ls-tree 10c195f4f039d79a0441fefb0e63e07d227edb89
    100644 blob d3f48b93b168b70f7bf91e27e6bbf0ef97d52821    README
                ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    $ git ls-tree 56b93cce25073a26c67c07d7fe0b744668bf0d32
    100644 blob d3f48b93b168b70f7bf91e27e6bbf0ef97d52821    TOM
                ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^    ^^^

    The tree-level sha1 takes the sub-component names into account...
    but the blob computation doesn't
    ...it's only on file size/contents

    (i'm not sure about file mode...but you get the point)

!SLIDE smbullets incremental
# trees
* like directories, contents can be other trees or blobs
* sha1s computed off of sub-components' sha1s/names
* difference in tree sha1s means they have different content
* (that last one is important)
