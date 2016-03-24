# git-map

run an arbitrary command against all commits, or *n* evenly-spaced commits across time.

### examples

Count number of files for every commit:

```
git-map "git ls-files | wc -l | xargs"
```

Count lines of code for 10 evenly-spaced commits across time (excluding a few directories):

```
git-map "grep '' -IR . --exclude-dir={.git,log,vendor} | wc -l | xargs" -n 10
```
