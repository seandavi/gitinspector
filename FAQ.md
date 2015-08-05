**Q:** In our project, someone accidently used two different e-mail
addresses when commiting and now we have duplicates for the same user shown by the generated gitinspector statistics.

A: This can easily happen. Luckily, git itself (not gitinspector) offers a solution via the use of a '.mailmap' file. See https://www.kernel.org/pub/software/scm/git/docs/git-shortlog.html#_mapping_authors for more information.


---


**Q:** My insertions minus deletions in the statistics does not equal the number of rows that have survived. There must be something wrong with the statistics!

A: Probably not. The number of surviving rows will usually be different because the contributions from other authors will interfere with the statistics. Some other author might for example remove lines that you have written, or maybe you moved some of their code from one file to another?

Also, an insertion isn't strictly the same thing as the actual number of rows attributed to an author. When committing code, git will check for duplicates from other files and also check if a newly added file is a copy of some other file. If copies are detected; the author might not get the insertions but may still get some of the rows attributed to him or her.


---


**Q:** When showing responsibilities (via the -r flag), gitinspector shows that I am responsible for rows in a file (or files) that I have never edited. How can this be?

A: This is normal and probably means that someone else in the development team moved (or created) rows in that file from code originally written by you.


---


**Q:** How do I tell gitinspector to pass it's output to a file instead of the terminal? This would be very useful when outputting HTML. There doesn't seem to be any command-line parameter for this?

A: There isn't. You can just use the terminal to redirect stdout to a file. This can be done in most terminals by supplying ">". For example; passing the command "gitinspector -F html /path/to/git/repo > statistics.html" would write the gitinspector HTML output to the file "statistics.html" in the current directory.


---


**Q:** When running gitinspector; i get a UnicodeEncodeError exception.

A: This usually means that your terminal has an incompatible encoding configured that is unable to print out the characters being sent to it by gitinspector. See [issue 9](https://code.google.com/p/gitinspector/issues/detail?id=9) for more information on this topic. Redirecting the output of gitinspector to a file should also solve the issue.


---


**Q:** When generating a HTML page with the -r flag, the number of minor authors in the responsibilities view does not equal the number of minor authors in the blame view. In fact, there are less minor authors in the responsibilities view. Strange things happen when generating text and HTML output also; some authors responsibilities are never shown at all. How is this possible?

A: Because the responsibilities view filters out any authors that only have lines inside comments. The responsibilities view calculates responsibilities by ELOC (Estimated-Lines-Of-Code). You can, in fact, even get a major author filtered out and not even shown if that author only has lines inside comments.


---


**Q:** The stability value introduced in the new master branch of gitinspector shows a value above 100% for one of the authors in the repository! How is this possible?

A: This can happen when somebody else inserts code that git attributes to the author in question. In other words, it considers this author to be the original writer of the inserted rows.