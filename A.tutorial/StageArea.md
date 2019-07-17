# Staged Area

```bash
git ls-files -s
```


```bash
$ git cat-file -p 68aba6
100644 blob 3b18e512dba79e4c8300dd08aeb37f8e728b8dad    hello.txt
```

The contents of the object should be easy to interpret. The first number, `100644`, represents the file attributes of the object in octal, which should be familiar to anyone who has used the Unix `chmod` command. Here, `3b18e5` is the object name of the `hello world` blob, and `hello.txt` is the name associated with that blob.



