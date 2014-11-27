
This repository is here only for historical use, no real development will
happen here.  [otr4j][] was for a while developed as part of the
[ChatSecureAndroid][] source.  Those commits were extracted out of the
ChatSecureAndroid git repo, then grafted onto the old otr4j git repo at an
appropriate place in the history.  The current place for [otr4j][] development
is [here][otr4j].

This git repo is to smooth the process of integrating these commits into the
work done by redsolution, jitsi, and others.

Here's the general idea of the grafting process:

1- get the commits from ChatSecureAndroid.git:
```
cd /tmp
git clone https://github.com/guardianproject/ChatSecureAndroid.git
cd ChatSecureAndroid
git filter-branch --subdirectory-filter src/net --prune-empty -- --all
git filter-branch --index-filter 'git ls-files -s | sed "s-java/-src/net/java/-" | GIT_INDEX_FILE=$GIT_INDEX_FILE.new  git update-index --index-info && mv "$GIT_INDEX_FILE.new" "$GIT_INDEX_FILE"' HEAD
```

2- get otr4j for grafting onto:
```
git clone https://github.com/redsolution/otr4j.git
cd otr4j
git remote add ChatSecureAndroid /tmp/ChatSecureAndroid
git fetch ChatSecureAndroid
echo 'e72a144b109bb35edf55631c5012d6471e1473e0 5fe2968bfedbbcf4224c4052355011901ddd950e' > .git/info/grafts
git filter-branch
```


  [otr4j]: https://github.com/otr4j/otr4j
  [ChatSecureAndroid]: https://github.com/guardianproject/ChatSecureAndroid
