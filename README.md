## Pretty Word Diffs

GitHub has a nice way of showing word-based diffs on Markdown files. I needed a way to be able to create similar pretty diffs as standalone documents. This is what I came up with.  

### Requirements:

* git
* pandoc 


```
git clone https://github.com/jduckles/pwdiff
cd pwdiff 
./pwdiff examples/file1.md examples/file2.md > out.html
```
Then have a look at out.html and you should see something like:

![Pretty diffs](https://github.com/jduckles/pwdiff/blob/master/example/output.png?raw=true)


## How does this work?

1. We use git's [`--word-diff`](https://git-scm.com/docs/git-diff#Documentation/git-diff.txt---word-diffltmodegt) option. 
2. Which outputs `{+ +}` for additions and `[- -]` for removals
3. Using sed we replace addition and removal tags with markdown tags for underline and strikethrough respectively
4. We treat output as Markdown and pipe to pandoc to convert to HTML
5. Applying the `styles.css` to that HTML we style underline to green and strikethrough to red to show additions and removals in a colorblind accessible way

## Gotchas 

* We're using git diff's -U option to show so-many lines of context. I've set this very large for now. It should probably just be the larger of the total number lines of the two files input.
* This is fragile to the tagging syntax used by git diff ``[- -], {+ +}`` as we're using `sed` to replace those. If your workflow or text contains those strings, ymmv.
