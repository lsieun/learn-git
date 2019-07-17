# SHA-1

## What is a SHA-1 Hash?

A `SHA-1` hash is a secure hash digest function that is used extensively in Git.

> SHA-1, a secure hash digest function

It outputs a 160-bit (20-byte) hash value, which is usually displayed as a 40-character hexadecimal string.

> 160-bit = 20-byte = 40-character hexadecimal string

The full 40 characters are rather unwieldy, so Git often shows shortened `SHA-1`s (as long as they’re unique in the repository). Anywhere that Git accepts a `SHA-1` unique commit reference, it will also accept the shortened version (as long as the shortened version is still unique within the repository).

> long SHA-1 --> shortened SHA-1

## How to Calculate SHA-1

```bash
$ echo "hello world" > hello.txt
$ git hash-object hello.txt
3b18e512dba79e4c8300dd08aeb37f8e728b8dad
```

## Use Case

- tag
- commit
- tree
- blob

The hash is used to uniquely identify commits by Git by their contents and metadata. They’re used instead of incremental revision numbers (like in Subversion) due to the distributed nature of Git. 

When you commit locally, Git can’t know whether your commit occurred before or after another commit on another machine, so it can’t use ordered revision numbers.




