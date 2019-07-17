# git_commit

## Basic

```bash
git commit --message "Initial Commit"
```

The `--message` flag for git commit can be abbreviated to `-m` (all abbreviations use a single `-`). If this flag is omitted, Git opens a text editor (specified by the `EDITOR` or `GIT_EDITOR` environment variable) to prompt you for the commit message.

## Options

`git commit` can be called with `--author` and `--date` flags to override the auto-set metadata in the new commit.

## Output

```bash
## commit changes staged in the index
$ git commit --message "First Commit"
[master (root-commit) 804345e] First Commit
 1 file changed, 1 insertion(+)
 create mode 100644 hello.txt
```

- `master`: the name of the branch where the commit was made (the default, `master`)
- `root-commit`: It’s shown only for the first commit in a repository and means this commit has no parent.
- `804345e`: the shortened SHA1
- `First Commit`: the commit message
- `1 file changed, 1 insertion(+)`: the number of files changed and the number of lines inserted or deleted across all the files in this commit.
- `create mode 100644 hello.txt`: a new file was created, along with the Unix file mode ( 100644 )


```txt
[<branch_name> (root-commit) <shortened_sha1>] <commit_message>
 <file_number> file changed, <add_num> insertion(+), <del_num> deletion(-)
 create mode 100644 <file_name>
```

## Small Commits are better

Sometimes it’s desirable to pick only some changed files (or even some changed lines within files) to include in a commit and leave the other changes to be added in a future commit. **Commits should be kept as small as possible**. This allows their message to describe a single change rather than multiple changes that are unrelated but were worked on at the same time.

**Small commits keep the history readable**; it’s easier when looking at a small commit in the future to understand exactly why the change was made.

If a small commit is later found to be undesirable, it can be easily reverted. This is much more difficult if many unrelated changes are clumped together into a single commit and you wish to revert a single change.

## How Should Commit Message be Formatted

The commit message is structured like an email. The **first line** is treated as the **subject** and **the rest** as the **body**.

The **commit subject** is used as a summary for that commit when only a single line of the commit message is shown, and it should be 50 characters or less.

The **remaining lines** should be separated from **the subject** by **a single, blank line**.

The **remaining lines** should be wrapped at 72 characters or less. The commit message should describe what the commit does in as much detail as is useful, in the present tense.


