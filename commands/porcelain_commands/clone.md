# clone

## different protocol

`git clone`基本形式：

```bash
git clone <repository> <directory>
```

### ssh

```bash
git clone ssh://<username>@<server_name>:<port>/home/<username>/public_html
git clone ssh://<username>@<server_name>:<port>/home/<username>/public_html /home/user/workspace
```

示例

```bash
git clone ssh://tom@192.168.80.70:/home/tom/GitInPractice
git clone ssh://tom@192.168.80.70:/home/tom/GitInPractice ~/abc/xyz
```

### http

```bash
git clone https://github.com/lsieun/demo
```

