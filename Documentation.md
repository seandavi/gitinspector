# Requirements #

  * Git executable defined somewhere in your PATH, otherwise gitinspector will not be able to run git.
  * Python 2.6+.

# Running gitinspector #

The program can be executed using two different methods.
  1. By _changing directory_ to a GIT repository and running the command ```
gitinspector.py [OPTION]...```.
  1. By running the command ```
gitinspector.py [OPTION]... [GIT REPOSITORY]```

# The gitinspector options #

The gitinspector script itself accepts a number of options that modifies it's behaviour and how statistics are generated. It is possible to get a brief explanation of all available options by supplying **-h** or **--help** when running the program. Boolean arguments can only be given to long options.

The available options are:

| **-c, --checkout-missing[=BOOL]** | Deprecated since 0.3.2 | By default, gitinspector will just print out missing files in a list and skip the inclusion of certain statistics from those files. With this option, gitinspector will try to checkout any missing files before computing statistics. |
|:----------------------------------|:-----------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **-f, --file-types=EXTENSIONS**   |                        | A comma separated list of file extensions to include when computing statistics. The default file extensions used are: _java,c,cpp,h,hpp,py,glsl,rb,js,sql_.                                                                            |
| **-F, --format=FORMAT**           | New since 0.2.0        | Defines in which format output should be generated; the default format is _'text'_ and the available formats are: _html,htmlembedded,text,xml_.  <br><br>Please refer to the section <a href='#Supported_output_formats__(new_since_0.2.0).md'>#Supported_output_formats__(new_since_0.2.0)</a> for more information about the output formats. <br>
<tr><td> <b>--grading[=BOOL]</b>           </td><td> New since 0.2.0        </td><td> Show statistics and information in a way that is formatted for grading of student project; this is the same as supplying -HlmrTw.                                                                                                      </td></tr>
<tr><td> <b>-H, --hard[=BOOL]</b>          </td><td>                        </td><td> Track rows and look for duplicates harder. In essence, this passes additional -C (and -M) options to the git executable.                                                                                                               </td></tr>
<tr><td> <b>-l, --list-file-types[=BOOL]</b> </td><td>                        </td><td> List all the file extensions available in the current branch of the repository. This can be very useful when you want to check what extensions are available in the repository. These can later be passed to gitinspector using the <b>-f</b> or <b>--file-types</b> options. </td></tr>
<tr><td> <b>-L, --localize-output[=BOOL]</b> </td><td> New since 0.3.0        </td><td> By default; the generated statistics are always in English. This flag localizes the generated output to the selected system language if a translation is available.                                                                    </td></tr>
<tr><td> <b>-m, --metrics[=BOOL]</b>       </td><td>                        </td><td> Include checks for certain metrics during the analysis of commits. Currently very simple, but will be expanded.                                                                                                                        </td></tr>
<tr><td> <b>-r, --responsibilities[=BOOL]</b> </td><td>                        </td><td> Show which files the different authors seem most responsible for.                                                                                                                                                                      </td></tr>
<tr><td> <b>--since=DATE</b>               </td><td> New since 0.2.1        </td><td> Show statistics for commits more recent than a specific date. The date format is in approxidate; the same as the format used in git itself.                                                                                            </td></tr>
<tr><td> <b>-T, --timeline[=BOOL]</b>      </td><td>                        </td><td> Show commit timeline, including author names. the timeline shows a statistical analysis where the amount of changes is calculated in relation to all other changes made by all other authors a specific month. Using the <b>-w</b> option, it is possible to get this output specified in weeks instead.  </td></tr>
<tr><td> <b>--until=DATE</b>               </td><td> New since 0.2.1        </td><td> Show statistics for commits older than a specific date. The date format is in approxidate; the same as the format used in git itself.                                                                                                  </td></tr>
<tr><td> <b>--tda367</b>                   </td><td> Deprecated since 0.2.0 </td><td> Show statistics and information in a way that is formatted for the course TDA367/DIT211; this parameter equals -lmrTw.                                                                                                                 </td></tr>
<tr><td> <b>-w, --weeks[=BOOL]</b>         </td><td>                        </td><td> Show all statistical information in weeks instead of in months.                                                                                                                                                                        </td></tr>
<tr><td> <b>-x, --exclude=PATTERN</b>      </td><td>                        </td><td> An exclusion pattern describing file paths, file names, authors or emails that should be excluded from the statistics. Works in the same manner as an inverted grep, meaning that any matched file names will be excluded from the generated statistics. Can be specified multiple times. Please refer to the section <a href='#Filtering.md'>#Filtering</a> for more information on how to fully utilize filtering.<br><br>New since 0.3.0: Support for regular expressions.<br>New since 0.3.2: Support for filtering out commits from authors with a specific name or email. </td></tr>
<tr><td> <b>-h, --help</b>                 </td><td>                        </td><td> Display this help and exit.                                                                                                                                                                                                            </td></tr>
<tr><td> <b>--version</b>                  </td><td>                        </td><td> Output version information and exit.                                                                                                                                                                                                   </td></tr></tbody></table>

<h1>Supported output formats  (new since 0.2.0)</h1>
There are support for multiple output formats in gitinspector. They can be selected using the -F/--format flags when running the main gitinspector script.<br>
<blockquote><h2>Text (Plain Text)</h2>
Plain text with some very simple ANSI formatting, suitable for console output. This is the format chosen by default by gitinspector.<br>
<h2>HTML</h2>
HTML with external links. The generated HTML page links to some external resources; such as the JavaScript library JQuery. It requires an active internet connection to properly function. This output format will most likely also link to additional external resources in the future.<br>
<h2>HTMLEmbedded  (new since 0.3.0)</h2>
HTML with no external links. Similar to the HTML output format, but requires no active internet connection. As a consequence; the generated pages are bigger (as certain scripts have to be embedded into the generated output).<br>
<h2>XML</h2>
XML suitable for machine consumption. If you want to parse the output generated by gitinspector in a script or application of your own; this is the format you should choose.</blockquote>

<h1>Filtering</h1>

gitinspector offers several different ways of filtering out unwanted information from the generated statistics. As of version 0.3.2, the following filtering is supported:<br>
<pre><code>gitinspector -x myfile # filter out and exclude statistics from all files (or paths) with the string "myfile"</code></pre>
<pre><code>gitinspector -x file:myfile # filter out and exclude statistics from all files (or paths) with the string "myfile"</code></pre>
<pre><code>gitinspector -x author:John # filter out and exclude statistics from all authors containing the string "John"</code></pre>
<pre><code>gitinspector -x email:@gmail.com # filter out and exclude statistics from all authors with a gmail account</code></pre>
<blockquote><h2>Mixing several filters together</h2>
gitinspector lets you add multiple filtering rules by simply specifying the -x options several times or by separating each filtering rule with a comma;<br>
<pre><code>gitinspector -x author:John -x email:@gmail.com</code></pre>
<pre><code>gitinspector -x author:John,email:@gmail.com</code></pre>
<h2>Using regular expressions</h2>
Sometimes, sub-string matching (as described above) is simply not enough. Therefore, gitinspector let's you specify regular expressions as filtering rules. This makes filtering much more flexible. Here are some examples:</blockquote>

<blockquote><pre><code>gitinspector -x "author:^(?!(John Smith))" # only show statistics from author "John Smith"</code></pre>
<pre><code>gitinspector -x "author:^(?!([A-C]))" # only show statistics from authors starting with the letters A/B/C</code></pre>
<pre><code>gitinspector -x "email:.com$" # filter out statistics from all email addresses ending with ".com"</code></pre></blockquote>

<h1>Using git config to configure gitinspector (new since 0.3.0)</h1>

Options in gitinspector can be set using git config. Consequently, it is possible to configure gitinspector behavior globally (in all git repositories) or locally (in a specific git repository). It also means that settings will be permanently stored. All the long options that can be given to gitinspector can also be configure via git config (and take the same arguments).<br>
<br>
To configure how gitinspector should behave in all git repositories, execute the following git command:<br>
<br>
git config --global inspector.<b>option</b> <b>setting</b>

To configure how gitinspector should behave in a specific git repository, execute the following git command (with the current directory standing inside the repository in question):<br>
<br>
git config inspector.<b>option</b> <b>setting</b>

<h1>Windows support</h1>

If you want to run gitinspector under Windows, there are a few things to consider. Refer to the following page for more information:<br>
<br>
<a href='http://docs.python.org/using/windows.html'>http://docs.python.org/using/windows.html</a>