%% title: Rakudo Star 2012.11 released
%% date: 2012-11-28

On behalf of the Rakudo and Perl 6 development teams, I'm happy to announce the November 2012 release of "Rakudo Star", a useful and usable distribution of Perl 6.  The tarball for the November 2012 release is <a href="http://github.com/rakudo/star/downloads">available for download</a>.  A Windows .MSI version of Rakudo star will usually appear in the downloads area shortly after the tarball release.

In the Perl 6 world, we make a distinction between the language ("Perl 6") and specific implementations of the language such as "Rakudo Perl".  This Star release includes <a href="https://github.com/rakudo/rakudo/blob/master/docs/announce/2012.11 ">release 2012.11</a>of the <a href="http://github.com/rakudo/rakudo ">Rakudo Perl 6 compiler</a>, version 4.6.0 of the <a href="http://parrot.org/">Parrot Virtual Machine</a>, and various modules, documentation, and other resources collected from the Perl 6 community.

Some of the new features added to this release include:

<ul><li>heredocs</li>
<li>quote adverbs (like q:w//)</li>
<li>implemented precedence related traits (equiv, looser, tighter, assoc)</li>
<li>Perl 6 grammar NFAs are pre-computed, saving some work on each  invocation; this shaved around 10% off the time needed to run the spectests</li>
<li>regexes and quotes have better support for user-selected delimiters</li>
<li>FIRST/NEXT/LAST can now be used in all types of loop (previously limited to for)</li>
<li>several fixes related to module precompilation. This should make working with larger code bases much less painful.</li>

This release also contains a range of performance improvements, bug fixes, improvements to error reporting and better failure modes.

The following features have been deprecated or modified from previous releases due to changes in the Perl 6 specification, and are being removed or changed as follows:

<ul>
<li> at present, a reference to an &amp;foo that does not exist evalutes to Nil. This will become a CHECK-time failure, in line with STD.</li>
<li>Unary hyper ops currently descend into nested arrays and hashes.  This will change to make them equivalent to a one-level map.</li>
<li>~/.perl6/lib will go away from the default include path (@*INC).
  Instead %*CUSTOM_LIB now holds paths to four library locations:
<pre>
perl    Rakudo installs its core modules here
vendor  OS-level package managers should install their modules here
site    for local module installations (e.g. with panda or ufo)
home    like site, but always under the user's home directory.
        fallback if site isn't writable.
</pre>
</li>
<li>The Str.ucfirst builtin is deprecated; it will be replaced by Str.tc.</li>
<li> Leading whitespace in rules and under :sigspace will no longer be converted to &lt;.ws&gt; .  For existing regexes that expect this conversion, add a &lt;?&gt; in front of leading whitespace to make it meta again.</li>
<li>The ?-quantifier on captures in regexes currently binds the capture  slot to a List containing either zero or one Match objects; i.e., it is equivalent to "** 0..1".  In the future, the ?-quantifier will bind the slot directly to a captured Match or to Nil.  Existing code can manage the transition by changing existing ?-quantifiers to use "** 0..1", which will continue to return a List of matches.</li>
</ul>

There are some key features of Perl 6 that Rakudo Star does not yet handle appropriately, although they will appear in upcoming releases.  Some of the not-quite-there features include:

<ul>
  <li>advanced macros</li>
  <li>threads and concurrency</li>
  <li>Unicode strings at levels other than codepoints</li>
  <li>interactive readline that understands Unicode</li>
  <li>non-blocking I/O</li>
  <li>much of Synopsis 9</li>
</ul>

There is an online resource at http://perl6.org/compilers/features that lists the known implemented and missing features of Rakudo and other Perl 6 implementations.

In many places we've tried to make Rakudo smart enough to inform the programmer that a given feature isn't implemented, but there are many that we've missed.  Bug reports about missing and broken features are welcomed at <rakudobug@perl.org>.

See http://perl6.org/ for links to much more information about Perl 6, including documentation, example code, tutorials, reference materials, specification documents, and other supporting resources.  A draft of a Perl 6 book is available as docs/UsingPerl6-draft.pdf in the release tarball.

The development team thanks all of the contributors and sponsors for making Rakudo Star possible.  If you would like to contribute, see http://rakudo.org/how-to-help, ask on the perl6-compiler@perl.org mailing list, or join us on IRC #perl6 on freenode.
