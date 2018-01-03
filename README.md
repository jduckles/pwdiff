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

## Gotchas 

* We're using git diff's -U option to show so-many lines of context. I've set this very large for now. It should probably just be the larger of the total number lines of the two files input.
* This is fragile to the tagging syntax used by git diff ``[- -], {+ +}`` as we're using `sed` to replace those. If your workflow or text contains those strings, ymmv.
