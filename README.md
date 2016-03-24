# git-map

run an arbitrary command against all commits, or *n* evenly-spaced commits across time.

## examples

#### count number of files for every commit:

```
git-map "git ls-files | wc -l | xargs"
```

#### count lines of code for 10 evenly-spaced commits:

```
git-map "grep '' -IR . --exclude-dir={.git,log,vendor} | wc -l | xargs" -n 10
```

#### boot up webserver and take a screenshot for 5 evenly-spaced commits:

```
git-map "~/screenshot.sh" -n 5
```

```bash
# screenshot.sh

# Reinstall dependencies as they may be different for older commits
bundle install

# Boot up the server and record the process ID (so we can kill it later)
nohup bundle exec middleman >/dev/null 2>&1&
pid=$!

# Wait for the server to finish booting, then take a screenshot
sleep 5
open "http://localhost:4567"
sleep 5
timestamp=$(date +%s)
screencapture ~/Desktop/screenshot-$timestamp.jpg

kill $pid
```
