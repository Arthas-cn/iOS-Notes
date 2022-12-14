## OC代码格式化
+ 参考OC代码编写[Google规范](https://google.github.io/styleguide/objcguide.html)
+ 代码自动化插件[下载插件](https://github.com/square/spacecommander)
+ 代码Clang-format[语法参考](https://clang.llvm.org/docs/ClangFormatStyleOptions.html)

## 安装教程：
> 注意：该插件不能识别中文目录,所以项目中不能有中文目录

1、下载之后，在 目录，可以看到有以下文件：

+ setup-repo.sh 初始化
+ format-objc-file.sh 格式化单个文件
+ format-objc-files.sh 格式化所有暂存文件
+ format-objc-files-in-repo.sh 格式化整个仓库

2、在项目（这里的项目是我们开发的工程项目，例如Wocute、CHeart）的根目录，执行 setup-repo.sh 脚本。
在命令窗口cd到我们项目的根目录，把setup-repo.sh文件拖进窗口，按回车即可。

3、复制以下内容覆盖`.clang-format`文件
```
---
# `Language` intentionally left blank to apply these rules
# as the default formatting options.
# This addresses an issue which can occur when clang-format
# decides a header looks more like c++ than objc.

# BasedOnStyle:  Google
AccessModifierOffset: -1
ConstructorInitializerIndentWidth: 4
SortIncludes: false

AlignAfterOpenBracket: true
AlignEscapedNewlinesLeft: true
AlignOperands: false
AlignTrailingComments: true

AllowAllParametersOfDeclarationOnNextLine: false
AllowShortBlocksOnASingleLine: false
AllowShortCaseLabelsOnASingleLine: false
AllowShortIfStatementsOnASingleLine: true
AllowShortFunctionsOnASingleLine: All
AllowShortLoopsOnASingleLine: true

AlwaysBreakAfterDefinitionReturnType: false
AlwaysBreakTemplateDeclarations: false
AlwaysBreakBeforeMultilineStrings: false

BreakBeforeBinaryOperators: None
BreakBeforeTernaryOperators: false
BreakConstructorInitializersBeforeComma: false

BinPackArguments: true
BinPackParameters: true
ColumnLimit: 0
ConstructorInitializerAllOnOneLineOrOnePerLine: true
DerivePointerAlignment: false
ExperimentalAutoDetectBinPacking: false
IndentCaseLabels: true
IndentWrappedFunctionNames: false
IndentFunctionDeclarationAfterType: false
MaxEmptyLinesToKeep: 2
KeepEmptyLinesAtTheStartOfBlocks: false
NamespaceIndentation: Inner
ObjCBlockIndentWidth: 4
ObjCBreakBeforeNestedBlockParam: false
ObjCSpaceAfterProperty: true
ObjCSpaceBeforeProtocolList: true
PenaltyBreakBeforeFirstCallParameter: 10000
PenaltyBreakComment: 300
PenaltyBreakString: 1000
PenaltyBreakFirstLessLess: 120
PenaltyExcessCharacter: 1000000
PenaltyReturnTypeOnItsOwnLine: 200
PointerAlignment: Right
SpacesBeforeTrailingComments: 1
Cpp11BracedListStyle: true
Standard: Auto
IndentWidth: 4
TabWidth: 8
UseTab: Never
BreakBeforeBraces: Custom
BraceWrapping:
    AfterClass: true
    AfterControlStatement: false
    AfterEnum: false
    AfterFunction: false
    AfterNamespace: true
    AfterObjCDeclaration: true
    AfterStruct: false
    AfterUnion: false
    BeforeCatch: false
    BeforeElse: false
    IndentBraces: false
    SplitEmptyFunction: false

SpacesInParentheses: false
SpacesInSquareBrackets: false
SpacesInAngles: false
SpaceInEmptyParentheses: false
SpacesInCStyleCastParentheses: false
SpaceAfterCStyleCast: false
SpacesInContainerLiterals: true
SpaceBeforeAssignmentOperators: true

ContinuationIndentWidth: 4
CommentPragmas: "^ IWYU pragma:"
ForEachMacros: [foreach, Q_FOREACH, BOOST_FOREACH]
SpaceBeforeParens: ControlStatements
DisableFormat: false
---


```

## 忽略配置：
1. 忽略某个目录，在项目的根目录打开 .formatting-directory-ignore 文件，添加以项目为相对路径即可
2. 忽略某个文件，只需在需要忽略的文件的头部，注意是最头部。
添加 #pragma Formatter Exempt 或者// MARK: Formatter Exempt 即可
3. 忽略某段代码
```
// clang-format off 

用这两段包围的代码不会格式化

// clang-format on
```


## 代码格式化快捷命令
1. 进入用户根目录 `cd ~`
2. 打开.zshrc文件 `open .zshrc`
3. 添加以下内容，注意要将`/Users/xxx/xxx/spacecommander-master`替换成你本地的目录
```
alias ocfmstage="/Users/xxx/xxx/spacecommander-master/format-objc-files.sh -s"
alias ocfmfile="/Users/xxx/xxx/spacecommander-master/format-objc-file.sh"
alias ocfmall="/Users/xxx/xxx/spacecommander-master/format-objc-files-in-repo.sh"
```
4、重新打开terminal命令窗口 输入oc 再按Tab键即可看到提示

+ ocfmstage 命令是 格式化暂存文件
+ ocfmfile 命令是 格式化单个文件
+ ocfmall  命令是 格式化所有文件

> 注意这三个命令一定要在项目的根目录执行，否则会报错找不到repo

5、如果 不想要格式化文件 需要在git commit 后面加上 --no-verify 例如：
`git commit --no-verify -m "test"` 
