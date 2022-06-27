# 目录
- [VS Code快捷键自定义设置](#vs-code快捷键自定义设置)
- [复制当前行到上或下一行](#复制当前行到上或下一行)

## VS Code快捷键自定义设置

参考
- [VS Code插件开发教程（5） 命令的使用 Command](https://juejin.cn/post/6971645962976509965)
- [Key Bindings for Visual Studio Code](https://code.visualstudio.com/docs/getstarted/keybindings)

Viewing modified keybindings#
You can view any user modified keyboard shortcuts in VS Code in the Keyboard Shortcuts editor with the Show User Keybindings command in the More Actions (...) menu. This applies the @source:user filter to the Keyboard Shortcuts editor (Source is 'User').

keybindings.json

```
   {
    "key": "ctrl+;",
    "command":"type",
    "args": {"text": "();\n"},
    "when": "editorTextFocus && editorLangId == 'c' || editorTextFocus && editorLangId == 'cpp' || editorTextFocus && editorLangId == 'cuda-cpp'"
    } 

```

## 复制当前行到上或下一行

    //复制当前行到上一行
    alt+shift+上键
    //复制当前行到下一行
    alt+shift+下键 