---
title: sublime常用插件
comments: true
date: 2018-01-04 22:37:28
tags:
categories:
- 开发工具
---

sublime编辑器的常用快捷键和插件配置
<!--more-->

# 1 常用快捷键
## 1.1 选择类
* <kbd>Ctrl + D</kbd>：多选，按<kbd>Ctrl</kbd>+<kbd>K</kbd>可以跳过当前选择的一个，按<kbd>Ctrl</kbd>+<kbd>U</kbd>可以取消选中。
* Ctrl+A：全选。
* Ctrl+Shift+L：选择多行。
* Ctrl+J：多行合并。
* Ctrl+K+0：展开所有折叠代码。
* Ctrl+Enter：在下一行插入新行。
* Ctrl+Shift+Enter：在上一行插入新行。
* Shift+↑：向上选中多行。
* Shift+↓：向下选中多行。
* Shift+←：向左选中文本。
* Shift+→：向右选中文本。
* Ctrl+Shift+←：向左单位性地选中文本。
* Ctrl+Shift+→：向右单位性地选中文本。
* Ctrl+Shift+↑：将光标所在行和上一行代码互换（将光标所在行插入到上一行之前）。
* Ctrl+Shift+↓：将光标所在行和下一行代码互换（将光标所在行插入到下一行之后）。
* Ctrl+Alt+↑：向上添加多行光标，可同时编辑多行。
* Ctrl+Alt+↓：向下添加多行光标，可同时编辑多行。

## 1.2 编辑类
* Ctrl+J：多行合并。
* Ctrl+/：注释单行。
* Ctrl+Shift+/：注释多行。
* Ctrl+K+U：转换大写。
* Ctrl+K+L：转换小写。
* Ctrl+Z：撤销。
* Ctrl+Y：恢复撤销。

## 1.3 查找类
* Ctrl+F：查找关键字。
* Ctrl+P：打开搜索框。
 1. 输入当前项目中的文件名，快速搜索文件；
 2. 输入@和关键字，查找文件中函数名；
 3. 输入：和数字，跳转到文件中某行；
 4. 输入#和关键字，查找变量名。
* Ctrl+Shift+P：打开命令框。
* Ctrl+G：跳转到某行。
* Ctrl+R：查找函数。
* Ctrl+： 查找文件中的变量名、属性名等。

## 1.4 显示类
* Ctrl+K+B：开启/关闭侧边栏。
* Ctrl+PageDown：向左切换当前窗口的标签页。
* Ctrl+PageUp：向右切换当前窗口的标签页。
* Alt+Shift+1：窗口分屏，恢复默认1屏（非小键盘的数字）。
* Alt+Shift+2：左右分屏-2列。
* Alt+Shift+3：左右分屏-3列。
* Alt+Shift+4：左右分屏-4列。
* Alt+Shift+5 等分4屏。
* Alt+Shift+8：垂直分屏-2屏。
* Alt+Shift+9：垂直分屏-3屏。
* F11：全屏模式。
* Shift+F11：免打扰模式。

# 2 基本配置

* 我的配置

```json
{
	"color_scheme": "Packages/Color Scheme - Default/Monokai.tmTheme",
	"dpi_scale": 1.0,//防止中文文件名乱码
	"font_size": 15,//字体
	"ignored_packages":["Vintage"],
	"theme": "Seti.sublime-theme",//当前主题
	"draw_minimap_border":true,//右侧缩略图边框
	"highlight_line":true,//当前行标亮
    "caret_style":"smooth", // 设置光标闪动方式
	"save_on_focus_lost":true,//失去焦点后保存
	"auto_complete":false, //自动完成
	"word_wrap":false, //强制不换行
	"word_separators":"./\\()\"':,.;<>~!@#$%^&*|+=[]{}`~?",// 双击选中中划线
	"update_check":false //不检查更新
}
```

* 所有配置

```JSON
{
    // 设置文本区域颜色主题
    "color_scheme": "Packages/Color Scheme – Default/Monokai.tmTheme",
    // 设置字体和大小
    "font_face": "",
    "font_size": 10,
    // 有效选项有：no_bold不显示粗体字，no_italic不显示斜体字，no_antialias关闭反锯齿，gray_antialias开启反锯齿
    // subpixel_antialias和no_round是OS X系统独有的，gdi和directwrite是windows系统独有的
    "font_options": [],
    // 在文字上双击会全选当前的内容，如果里面出现以下字符，就会被截断
    "word_separators": "./\\()\"'-:,.;<>~!@#$%^&*|+=[]{}`~?",
    // 是否显示行号
    "line_numbers": true,
    // 是否显示行号边栏
    "gutter": true,
    // 行号边栏和文字的间距
    "margin": 4,
    // 是否显示代码折叠按钮
    "fold_buttons": true,
    // 除非鼠标悬停行号边栏，否则代码折叠按钮将隐藏
    "fade_fold_buttons": true,
    // 列显示垂直标尺，在中括号里填入数字，宽度按字符计算
    "rulers": [],
    // 是否打开拼写检查
    "spell_check": false,
    // Tab键制表符宽度
    "tab_size": 4,
    // 设为true时，缩进和遇到Tab键时使用空格替代
    "translate_tabs_to_spaces": false,
    // 否则作用于单个空格
    "use_tab_stops": true,
     // false时禁止在载入的时候检测制表符和空格
    "detect_indentation": true,
    // 按回车时，自动与制表位对齐
    "auto_indent": true,
    //针对C语言的
    "smart_indent": true,
    // 需要启用auto_indent
    "indent_to_bracket": false,
    // 显示对齐的白线是否根据回车、tab等操作自动填补
    "trim_automatic_white_space": true,
    // 是否自动换行，如果选auto，需要加双引号
    "word_wrap": auto,
    // 设置窗口内文字区域的宽度
    "wrap_width": 0,
    // 防止被缩进到同一级的字换行
    "indent_subsequent_lines": true,
    // 如果没有定义过，则文件居中显示
    "draw_centered": false,
    // 自动匹配引号，括号等
    "auto_match_enabled": true,
    // 拼写检查的单词列表路径
    "dictionary": "Packages/Language – English/en_US.dic",
    "spelling_selector": "markup.raw, source string.quoted - punctuation - meta.preprocessor.c.include, source comment - source comment.block.preprocessor, -(source, constant, keyword, storage, support, variable, markup.underline.link, meta.tag)",
    // 代码地图的可视区域部分是否加上边框，边框的颜色可在配色方案上加入minimapBorder键
    "draw_minimap_border": false,
    // 是否一直显示代码地图框
    "always_show_minimap_viewport": false
    // 突出显示当前光标所在的行
    "highlight_line": false,
    // 设置光标闪动方式
    "caret_style": "smooth",
    // 设置光标的尺寸
    "caret_extra_top": 0,
    "caret_extra_bottom": 0,
    "caret_extra_width": 0,
    // 是否特殊显示当前光标所在的括号、代码头尾闭合标记
    "match_brackets": true,
    // 设为false时，只有光标在括号或头尾闭合标记的两端时，match_brackets才生效
    "match_brackets_content": true,
    // 是否突出显示圆括号，match_brackets为true生效
    "match_brackets_square": true,
    // 是否突出显示大括号，match_brackets为true生效
    "match_brackets_braces": true,
    // 是否突出显示尖括号，match_brackets为true生效
    "match_brackets_angle": false,
    // html和xml下突出显示光标所在标签的两端，影响HTML、XML、CSS等
    "match_tags": true,
    // 全文突出显示和当前选中字符相同的字符
    "match_selection": true,
    // 设置每一行到顶部，以像素为单位的间距，效果相当于行距
    "line_padding_top": 0,
    // 设置每一行到底部，以像素为单位的间距，效果相当于行距
    "line_padding_bottom": 0,
    // 设置为false时，滚动到文本的最下方时，没有缓冲区
    "scroll_past_end": true,
    // 控制向上或向下到第一行或最后一行时发生什么
    "move_to_limit_on_up_down": false,
    // 按space或tab时，实际会产生白色的点（一个空格一个点）或白色的横线（tab_size设置的制表符的宽度），选中状态下才能看到
    // 设置为none时，什么情况下都不显示这些点和线
    // 设置为selection时，只显示选中状态下的点和线
    // 设置为all时，则一直显示
    "draw_white_space": "selection",
    // 制表位的对齐白线是否显示，颜色可在主题文件里设置（guide，activeGuide，stackGuide）
    "draw_indent_guides": true,
    // 制表位的对齐白线，draw_normal为一直显示，draw_active为只显示当前光标所在的代码控制域
    "indent_guide_options": ["draw_normal"],
    // 为true时，保存文件时会删除每行结束后多余的空格
    "trim_trailing_white_space_on_save": false,
    // 为true时，保存文件时光标会在文件的最后向下换一行
    "ensure_newline_at_eof_on_save": false,
    // 切换到其它文件标签或点击其它非本软件区域，文件自动保存
    "save_on_focus_lost": false,
    "atomic_save": false,
    // 编码时不能自动检测编码时，将自动检测ASCII, UTF-8 和 UTF-16
    "fallback_encoding": "Western (Windows 1252)",
    // 默认编码格式
    "default_encoding": "UTF-8″,
    // 包含空字节的文件被打开默认为十六进制
    "enable_hexadecimal_encoding": true,
    // 每一行结束的时候用什么字符做终止符
    "default_line_ending": "system",
    // 通过写入备用文件，然后将其重命名为原始文件
    "show_definitions": true,
    // 设置为enabled时，在一个字符串间按Tab将插入一个制表符
    // 设置为true时，按Tab会根据前后环境进行代码自动匹配填补
    "tab_completion": true,
    // 代码提示
    "auto_complete": true,
    // 代码提示的大小限制
    "auto_complete_size_limit": 4194304,
    // 代码提示延迟显示
    "auto_complete_delay": 50,
    "auto_complete_selector": "meta.tag - punctuation.definition.tag.begin, source - comment - string.quoted.double.block - string.quoted.single.block - string.unquoted.heredoc",
    // 触发代码提示的其他情况
    "auto_complete_triggers": [ {"selector": "text.html", "characters": "<"} ],
    // 设false时，选择提示的代码按enter或点击可以自动补全，设true时将自动直接换行，功能由tab键替换
    "auto_complete_commit_on_tab": false,
    // 控制是否在代码段处于活动状态时自动完成
    // 仅当auto_complete_commit_on_tab为true有效。
    "auto_complete_with_fields": false,
    // 控制当选择自动完成窗口中第一个元素时会发成什么：设false时，窗口将隐藏，否则将选中最后一个元素
    "auto_complete_cycle": false,
    // 当输入</时，自动闭合HTML或XML标签
    "auto_close_tags": true,
    // 设置为false，使用Shift + tab总是插入制表符
    "shift_tab_unindent": false,
    // 设true时，在当前行，复制和剪切命令会分开
    "copy_with_empty_selection": true,
    // 选中的文本按Ctrl + f时，自动复制到查找面板的文本框里
    "find_selected_text": true,
    // 设true时，选中多行文本后，"Find in Selection"标志将自动启用
    "auto_find_in_selection": false,
    // 设true时，点击所选文本将开始拖放操作，Linux下不可用
    "drag_text": true,
    // 主题
    "theme": "Default.sublime-theme",
    // 滚动的速度
    "scroll_speed": 1.0,
    // 左边边栏文件夹动画
    "tree_animation_enabled": true,
    // 控制应用程序的动画
    "animation_enabled": true,
    // 高亮修改过的选项卡
    "highlight_modified_tabs": false,
    // 标签页的关闭按钮
    "show_tab_close_buttons": true,
    // 加粗侧边栏文件标签
    "bold_folder_labels": false,
    // 针对OS X
    "use_simple_full_screen": false,
    // 针对OS X
    "gpu_window_buffer": "auto",
    // 水平垂直滚动条：system和disabled为默认显示方式，enabled为自动隐藏显示
    "overlay_scroll_bars": "system",
    // 允许选项卡左右滚动
    "enable_tab_scrolling": true,
    // 状态栏显示文件编码
    "show_encoding": false,
    // 状态栏显示行结束
    "show_line_endings": false,
    // 热推出功能！退出时不会提示是否保存文件，而是直接退出
    // 下次打开软件时，文件保持退出前的状态，没来得及保存的内容都在，但并没有真实的写在原文件里
    "hot_exit": true,
    // 全屏模式退出时，下次将以全屏模式启动
    "remember_full_screen": false,
    // 重载文件前始终提示，即使文件未被修改。
    // 默认情况下，文件尚未编辑将自动重载，如果尚未保存修改将始终显示提示。
    "always_prompt_for_file_reload": false,
    // 针对OS X
    "open_files_in_new_window": true,
    // 针对OS X
    "create_window_at_startup": true,
    // 设true时，一但最后一个文件关闭将关闭程序窗口，除非窗口中打开了文件夹。
    "close_windows_when_empty": false,
    // 标题栏显示完整路径
    "show_full_path": true,
    // 显示构建结果面板，设false时，则通过"Tools/Build Results"菜单显示
    "show_panel_on_build": true,
    // 在发生错误的行下显示构建错误
    "show_errors_inline": true,
    // 单机侧边栏文件可预览，双击或编辑预览将打开文件分配选项卡
    "preview_on_click": true,
    // 哪些文件会被显示到侧边栏文件夹中
    "folder_exclude_patterns": [".svn", ".git", ".hg", "CVS"],
    "file_exclude_patterns": ["*.pyc", "*.pyo", "*.exe", "*.dll", "*.obj","*.o", "*.a", "*.lib", "*.so", "*.dylib", "*.ncb", "*.sdf", "*.suo", "*.pdb", "*.idb", ".DS_Store", "*.class", "*.psd", "*.db", "*.sublime-workspace"],
    // 以下二进制文件仍将显示在侧边栏中，但不会包含在Goto/Goto Anything或Find in Files中
    "binary_file_patterns": ["*.jpg", "*.jpeg", "*.png", "*.gif", "*.ttf", "*.tga", "*.dds", "*.ico", "*.eot", "*.pdf", "*.swf", "*.jar", "*.zip"],
    // 文件索引
    "index_files": true,
    // 设置用于索引的编码线程。
    // 值为0将使Sublime 基于数量猜测，使用index_files将禁用所有工作
    "index_workers": 0,
    // 指示哪些文件不用索引
    "index_exclude_patterns": ["*.log"],
    // 删除你想要忽略的插件，需要重启, 去掉Vinage开启vim模式
    "ignored_packages": ["Vintage"]
}
```

# 3 常用插件

## 3.1 网址
* [插件官网](https://packagecontrol.io/)
* [github总结](https://github.com/jikeytang/sublime-text)
* [简书总结](http://www.jianshu.com/p/e506c76bdc3b)
* [博客](http://www.cnblogs.com/hykun/p/sublimeText3.html)
* [视频教程](http://www.imooc.com/learn/333)
* [简书专题](http://www.jianshu.com/c/1627f31c077b)
* [学习资源篇](http://www.jianshu.com/p/d1b9a64e2e37)
* [增强篇](http://www.jianshu.com/p/5905f927d01b)
* [Markdown篇](http://www.jianshu.com/p/aa30cc25c91b)
* [主题篇](http://www.jianshu.com/p/13fedee165f1)
* [Git篇](http://www.jianshu.com/p/3a8555c273d8)
* [小技巧篇](http://www.jianshu.com/p/c75d21d2e967)

## 3.2 主题
* [参考](http://www.jianshu.com/p/13fedee165f1)
* [颜色主题汇总网站](http://colorsublime.com/)
* [主题排行](https://scotch.io/bar-talk/best-sublime-text-3-themes-of-2015-and-2016)
* [Seti_UI](https://packagecontrol.io/packages/Seti_UI)
* [Babel](https://packagecontrol.io/packages/Babel)

 ------- 分割线以上为推荐设置-----

* [Material Theme](https://packagecontrol.io/packages/Material%20Theme)
* [Boxy Theme](https://packagecontrol.io/packages/Boxy%20Theme)

## 3.3 编辑器功能
* [SideBarEnhancements](https://github.com/titoBouzout/SideBarEnhancements) 扩展侧边栏右键功能
* [sublime_terminal](https://github.com/wbond/sublime_terminal) 在sublime中打开windows命令窗口 <kbd>Ctrl+Shift+P</kbd> 或右键菜单
* [FindKeyConflicts](https://github.com/skuroda/FindKeyConflicts) 快捷键冲突检查
* [Diffy](https://github.com/zsong/diffy) 文件比较

------- 分割线以上为推荐设置-----

* [ChineseLocalization](https://github.com/rexdf/ChineseLocalization) 汉化插件
* [SideBarFolders](https://github.com/titoBouzout/SideBarFolders) 菜单位置管理侧边栏
* [SublimeSyncedSidebarBg](https://github.com/aziz/SublimeSyncedSidebarBg) 更改侧边栏颜色
* [Sublime-AdvancedNewFile](https://github.com/skuroda/Sublime-AdvancedNewFile) 创建新文件
* [IMESupport](https://github.com/chikatoike/IMESupport) 输入法输入栏光标位置
* [PlainTasks](https://github.com/aziz/PlainTasks) 计划任务
* [Nettuts-Fetch](https://github.com/weslly/Nettuts-Fetch) 获取最新版本的远程文件或zip包
* [Sublime-MultiEditUtils](https://github.com/philippotto/Sublime-MultiEditUtils) 扩展行列操作
* [SublimeServer](https://github.com/learning/SublimeServer) HTTP服务器
* [RemoveDuplicateCharacters](https://github.com/xianghongai/RemoveDuplicateCharacters) Sublime Text 删除重复字符

## 3.4 Git支持
* [GitGutter](https://github.com/jisaacks/GitGutter) 实时监测文件的变化
* [SublimeGit](https://github.com/SublimeGit/SublimeGit/) SublimeGit
* [sublimerge](https://packagecontrol.io/packages/Sublimerge%203) 比较工具
* [sublime-github](https://github.com/bgreenlee/sublime-github)与GitHub网站紧密联系，可以直接在Sublime中打开与GitHub关联的网址

------- 分割线以上为推荐设置-----

* [GitSavvy](https://github.com/divmain/GitSavvy) SublimeGit的同类竞品
* [Sublime-Gitignore](https://github.com/kevinxucs/Sublime-Gitignore) 一键生成忽略文件
* [gitconfig-sublimetext](https://github.com/robballou/gitconfig-sublimetext) 设置.gitignore和.gitconfig等文件语法高亮
* [SideBarGit](https://github.com/titoBouzout/SideBarGit) 在侧边栏的右键上增加Git常用操作
* [github-tools](https://github.com/temochka/sublime-text-2-github-tools)
* [github-sublime-theme](https://github.com/AlexanderEkdahl/github-sublime-theme) 一款GitHub主题
* [sublime-GitConflictResolver](https://github.com/Zeeker/sublime-GitConflictResolver) 用以解决在Merge过程中产生的冲突用
* [sublimerge](http://www.sublimerge.com/) 比较工具


## 3.5 文档美化
* [Sublime-HTMLPrettify](https://github.com/victorporof/Sublime-HTMLPrettify) 格式化HTML/CSS/JS代码
* [Pretty JSON](https://github.com/dzhibas/SublimePrettyJson) JSON格式化
* [ColorPicker](https://github.com/weslly/ColorPicker) 颜色选择器
* [ColorHighlighter](https://github.com/Monnoroch/ColorHighlighter) 颜色代码对应色彩显示
* [BracketHighlighter](https://github.com/facelessuser/BracketHighlighter) 高亮html标签、匹配括号、引号
* [TrailingSpaces](https://github.com/SublimeText/TrailingSpaces) 删除空白字符
* [CSSO](https://packagecontrol.io/packages/CSSO) css minify

------- 分割线以上为推荐设置-----

* [Sublime-CSS-Format](http://mutian.github.io/Sublime-CSS-Format/) CSS格式化
* [JsFormat](https://github.com/jdc0589/JsFormat) JS格式化
* [Tag](https://github.com/titoBouzout/Tag) 标签操作
* [sublime_DeleteBlankLines](https://github.com/NicholasBuse/sublime_DeleteBlankLines) 删除空行
* [sublime_alignment](https://github.com/wbond/sublime_alignment) 等号、冒号对齐

## 3.6 代码智能提示、补全与响应，代码模板
* [Emmet](https://emmet.io/) HTML/CSS代码快速编写
* [SublimeCodeIntel](http://sublimecodeintel.github.io/SublimeCodeIntel/) 代码智能提示补全 <kbd>Alt+Click</kbd>跳到定义；<kbd>Shift+Control+Space</kbd>列出可选项。
* [Sublime-Better-Completion](https://github.com/Pleasurazy/Sublime-Better-Completion) 较全的各种提示
* [SublimeAllAutocomplete](https://github.com/alienhard/SublimeAllAutocomplete) 代码自动完成
* [DocBlockr](https://github.com/spadgos/sublime-jsdocs) 注释编辑  <kbd>/**+Tab</kbd>
* [Autoprefixer](https://github.com/sindresorhus/sublime-autoprefixer) 补全CSS前缀
* [Markdown-preview](https://github.com/revolunet/sublimetext-markdown-preview) Markdown预览
* [AutoFileName](https://github.com/BoundInCode/AutoFileName) 文件路径自动提示 <kbd>Ctrl+Space</kbd>

------- 分割线以上为推荐设置-----

* [LiveStyle](http://livestyle.io/) 双向编辑样式
* [CSS3](https://github.com/y0ssar1an/CSS3) CSS3提示
* [FileHeader](https://github.com/shiyanhui/FileHeader) 根据文件扩展名创建模板
* [MarkdownEditing](https://github.com/SublimeText-Markdown/MarkdownEditing) Markdown语法支持

## 3.7 语法检测，代码测试
* [SublimeLinter3](https://github.com/SublimeLinter/SublimeLinter3) 语法及风格校验框架
* [SublimeLinter-jshint](https://github.com/SublimeLinter/SublimeLinter-jshint) JS语法及风格校验
* [SublimeLinter-csslint](https://github.com/SublimeLinter/SublimeLinter-csslint) CSS语法及风格校验
* [SublimeHttpRequester](https://github.com/braindamageinc/SublimeHttpRequester) 测试HTTP请求

## 3.8 文档编码
* [ConvertToUTF8](https://github.com/seanliang/ConvertToUTF8)
* [Hasher](https://github.com/dangelov/hasher) 符号编码转换

## 3.9 文件操作
* [SFTP](https://packagecontrol.io/packages/SFTP)
