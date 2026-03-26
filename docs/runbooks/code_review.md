Code review
Reviewing even the largest pull requests can be a manageable, straightforward process if you are able to evaluate changes on a commit-by-commit basis. Each of the guidelines detailed earlier focuses on making the commits readable; to extract information from commits, you can use the guidelines as a template.

Determine the narrative by reading the pull request description and list of commits. If the commits seem to jump between topics or address, leave a comment asking for clarification or changes.
Lightly scan the message and contents of each commit, starting from the beginning of the branch. Verify smallness and atomicity by checking that the commit does one thing and that doesn’t include any incomplete implementations. Recommend splitting or combining commits that are incorrectly scoped.
Thoroughly read each commit. Ensure the commit message sufficiently explains the code by first checking that implementation matches the intent, then that the code matches the stated implementation. Use the context and justification to guide your understanding of the code. If any of the requisite information is missing, ask for clarification from the author.
Finally, with a complete mental model of the commit’s changes and the overarching narrative, confirm the code is efficient and bug-free.

Finding bugs with git bisect
If you’ve ever found yourself with a broken deployment and no idea when the breakage was introduced, git bisect is the tool for you. Specifically, git bisect is a tool built into Git that, when given a known-good commit (for example, your last stable deployment) and a known-bad commit (the broken one), will perform a binary search of the commits in the middle to find which one introduced the error.


As useful as git bisect is, it absolutely requires that each commit it traverses is both atomic and small. If not atomic, you will be unable to test for repository stability at each commit; if not small, the source commit of your bug may be so large that you end up inefficiently reading code line-by-line to find the bug anyway.

