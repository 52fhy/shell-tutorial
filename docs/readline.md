# 行操作

Bash 内置了 Readline 库。命令行因此具有了这个库提供的很多“行操作”的功能，比如命令的自动补全。

Bash 允许关闭这个库。

```bash
$ bash --noediting
```

上面命令中，`--noediting`参数关闭了 Readline，启动的 Bash 就不带有行操作功能。

## 光标移动

Readline 提供了许多快捷键，用来快速地启动光标。

- `Ctrl a` 光标移到行首
- `Ctrl e` 光标移到行尾
- `Ctrl f` 光标向右（向前）移动一个字符（forward），与右箭头作用相同
- `Ctrl b` 光标向左（向后）移动一个字符（back），与左箭头作用相同
- `Alt f` 光标向右（向前）移动到词尾
- `Alt b` 光标向左（向后）移动到词首

上面的快捷键用到`Ctrl`键和`Alt`键，其中`Alt`键也可以用`Esc`键代替。

### 清除屏幕

`Ctrl l`快捷键可以清除屏幕，与`clear`命令作用相同。

## 编辑操作

下面的快捷键可以编辑命令行内容。

- `Ctrl-d` 删除光标位置的字符（delete）
- `Ctrl-w` 删除光标前面的单词
- `Ctrl-t` 光标位置的字符与它前面一位的字符交换位置（transpose）
- `Alt-t` 光标位置的词与它前面一位的词交换位置（transpose）
- `Alt-l` 将光标位置至词尾转为小写（lowercase）
- `Alt-u` 将光标位置至词尾转为大写（uppercase）

剪切和粘贴快捷键如下。

- `Ctrl k` 剪切光标位置到行尾的文本
- `Ctrl u` 剪切光标位置到行首的文本
- `Alt d` 剪切光标位置到词尾的文本
- `Alt Backspace` 剪切光标位置到词首的文本
- `Ctrl y` 在光标位置粘贴文本

同样地，Alt 键可以用 Esc 代替。

## 自动补全

命令输入到一半的时候，可以按一下`tab`键，Readline 会自动补全命令或路径。

如果符合条件的命令或路径有多个，就需要连续按两次`tab`键，Readline 会显示所有符合条件的命令或路径，用来提示。

除了命令或路径，`tab`还可以补全其他值。如果一个值以`$`开头，则按下`tab`键会补全变量；如果以`~`开头，则补全用户名；如果以`@`开头，则补全主机名（hostname），主机名以列在`/etc/hosts`文件里面的主机为准。

`Alt + Shift + ?`也会列出可能的补全，与连按两次`tab`键作用相同。`Alt + Shift + *`在命令行一次性插入所有可能的补全。

## 操作历史

Bash 的操作历史存放在用户主目录的`.bash_history`文件中，默认储存500个操作。

`history`命令用来展示这个文件。

```bash
$ history | less
```

如果想要搜索或执行某个以前的命令，可以像下面这样操作。

```bash
# 搜索某个命令
$ history | grep /usr/bin
```

上面命令返回`.bash_history`里面，那些包含`/usr/bin`的命令。

还有一种更简便的搜索方式，就是按下`Ctrl - r`，然后每键入一个字符，Shell 就会自动在历史文件中，查询并显示匹配的结果。这时，上下移动选中想要执行的命令，按下回车键即可。

下面是一些与操作历史相关的快捷键。

- `Ctrl - p` 显示上一个命令，与向上箭头效果相同（previous）
- `Ctrl - n` 显示下一个命令，与向下箭头效果相同（next）
- `Alt - <` 显示第一个命令
- `Alt - >` 显示最后一个命令，即当前的命令
- `Ctrl - o` 执行历史文件里面的当前条目，并自动显示下一条命令。这对重复执行某个序列的命令很有帮助。

感叹号可以用于执行历史文件里面的命令。如果想要执行`.bash_history`里面的第88个命令，可以像下面这样操作。

```bash
$ !88
```

感叹号的快捷键说明如下。

- `!!` 执行上一个命令
- `![number]` 执行历史文件里面指定行号的命令
- `![string]` 执行上一个以指定字符串开头的命令
- `!?[string]` 执行上一个包含指定字符串的命令

