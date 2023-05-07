git-rej-merge
=============

Working with merge conflicts has always been a pain for me, and sadly none of
the available tools have been sucessful in helping me understand what's
actually going on.

I've always been happier working with .rej files and that's what prompted this
small script.

Git-rej-merge will apply the merge and start `vim` with the target file and the
rejected chunks.


Usage
-----

Using git-rej-merge is as simple as adding it to your git config.

```
$ git config mergetool.rej-merge.cmd '<path/to>/git-rej-merge $BASE $LOCAL $REMOTE $MERGED'
$ git config merge.tool rej-merge
```

Next time you get a conflict, just use `git mergetool` (or `git mergetool
--tool=rej-merge` if you haven't set it as your default)

It will apply a three-way merge to the file and open a 4 pane vim instance.

```
.___________________.
|            |      |
| A          | B    |
|            |______|
|            |      |
|            | C    |
|            |______|
|            |      |
|            | D    |
|____________|______|
```

- Pane A is the merged file without the rejected chunks applied.
- Pane B holds all the chunks that couldn't be applied.
- Pane C and D contains commits and/or logs which could be useful in
  determining how and why the conflict(s) occured.

Manually edit the file in window A and use the B, C and D buffers. I commonly
lift the chunk from B over to A, and continue until I've cleared out the chunks
in B.

Then just save and quit Vim, the script will ask you if the merge was
successful, it doesn't care about the exit status of vim. If you answer `n`
you'll get a copy of the A pane with a `.work_in_progress` extension in your
repo.


Bugs
----

Most likely. If I recall correctly, it doesn't do well with file deletions.


License
------
git-rej-merge is in the public domain.
See UNLICENSE or http://unlicense.org for more information.


Contributing
------------
Contributions are probably welcome. This tool is highly biased for my workflow,
my system, my needs.
