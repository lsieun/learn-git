# config

## Telling Git Who You Are

One of the first things that you need to configure in Git is who you are, in terms of the username and e-mail address. Git expects you to set these two values, regardless of what interface or version of Git you use. This is because Git is a source management system. Because its purpose is to track changes by users over time, it wants to know who is making those changes so that it can record them.

The values can be set via commands:

```bash
git config --global user.name <name>
git config --global user.email <email address>
```

**The e-mail address is not validated** when you set it in Git. In fact, you can enter any e-mail address and Git will be happy. However, there is some advanced functionality in Git that uses this e-mail address. That functionality allows for tasks such as creating and sharing patches and zipped versions of changes. For that functionality, **having a correct e-mail address is important**. Also, there are other tools, such as Gerrit (a code-review tool built on top of Git), that heavily utilize the e-mail address and depend on it being correct.

使用email的时候，可以不用写对。但是，写对了，是有好处的。











