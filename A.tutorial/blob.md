# blob sha1

Git prefixes the object with "blob ", followed by the length (as a human-readable integer), followed by a NUL character

```bash
$ echo -e 'blob 12\0hello world' | sha1sum
3b18e512dba79e4c8300dd08aeb37f8e728b8dad  -
```

Source: http://alblue.bandlem.com/2011/08/git-tip-of-week-objects.html

How does GIT compute its commit hashes

```txt
Commit Hash (SHA1) = SHA1("blob " + <size_of_file> + "\0" + <contents_of_file>)
```

The text `blob⎵` is a constant prefix and `\0` is also constant and is the `NULL` character. The `<size_of_file>` and `<contents_of_file>` vary depending on the file.

## 计算一个文件的SHA1值

```bash
git hash-object hello.txt
```

