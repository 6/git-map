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

Boot up server and take a screenshot for 5 evenly-spaced commits across time:

```
git-map "~/screenshot.sh" -n 5
```

```bash
# screenshot.sh
nohup bundle exec middleman >/dev/null 2>&1&
pid=$!
sleep 5
open "http://localhost:4567"
sleep 5
timestamp=$(date +%s)
screencapture ~/Desktop/screenshot-$timestamp.jpg
kill $pid
```
