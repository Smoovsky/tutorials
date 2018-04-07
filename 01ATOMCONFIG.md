# 使用ATOM编辑器进行babel(ES6/ES7)，React开发的插件配置

## 写在前面
这是本专栏/公众号/简书的第一篇文章，所以也就打算写一篇比较“像是第一篇文章”的文章。
虽然说是第一次，但是如果初次接触web开发，那么我并不推荐使用ATOM, VS Code这类可以高度自定义的编辑器。如果正在熟悉基础的HTML+CSS & JavaScript，WebStorm应该是最好的选择。

## 概览
1. 插件安装
2. 插件配置

### 插件安装
需要的插件的包括如下：
* language-babel （注意，不推荐使用react插件，language-babel可以完全替代react插件）
* linter-eslint
* prettier-atom

### 插件配置

#### language-babel
language-babel的配置完全可以随个人喜好，本身自带的补完JSX内HTML标签，自动缩进等功能已经算很好用了。

#### linter-eslint
linter-eslint的配置步骤稍微繁琐一些。
1. 在全局安装eslint, eslint-plugin-react, babel-eslint(也可以使用每个project内部的这些包，一般可以全局安装)
运行：
 `npm install -g eslint eslint-plugin-react babel-eslint`

2. 对linter-eslint进行设置，以下设置也可以**直接在Atom里的插件设置**完成：

   - 1.找到：
  `C:\Users\[user name]\.atom\config.cson`
        - MAC和Linux的请自行寻找配置文件的路径
        - 替换[user name]为你的用户名

   - 2.为`"linter-eslint"`栏添加如下设置：
        -  ```
            "linter-eslint":
                disableWhenNoEslintConfig: false
                eslintrcPath: "C:\\Users\\[user name]\\"
                globalNodePath: "C:\\Program Files\\nodejs"
            ```
        - eslintrcPath将是存放es-lint配置文件的路径，一般选择自己的用户文档
        - 替换[user name]为你的用户名
        - globalNodePath是nodejs的安装路径

3. 配置eslint:  
创建`.eslintrc.json`并将下面的配置内容黏贴进去:  
   -  ```
        {
            "env": {
                "browser": true,
                "es6": true
            },
            "extends": ["eslint:recommended", "plugin:react/recommended"],
        	"parser": "babel-eslint",
            "parserOptions": {
                "ecmaFeatures": {
                    "experimentalObjectRestSpread": true,
                    "jsx": true
                },
                "sourceType": "module"
            },
            "plugins": [
                "react"
            ],
            "rules": {
                "indent": [
                    "error",
                    2,
        			{ "SwitchCase": 1 }
                ],
                "linebreak-style": [
                    "error",
                    "windows"
                ],
                "quotes": [
                    "error",
                    "single"
                ],
                "semi": [
                    "error",
                    "always"
                ],
        		"react/prop-types": [
        			0
        		],
        		"strict": 0
            }
        }
      ```
把`.eslintrc.json`放置到`C:\\Users\\[user name]\\`目录下。  
说明：  
   - 1.`"parser": "babel-eslint"`:使用babel-eslint作为parser，因为默认的parser不支持很多将要加入的特性，比如类在constructor外的地方初始化变量，直接在类里面声明箭头函数等等。
   - 2.`"extends": ["eslint:recommended", "plugin:react/recommended"]`加载linter的react插件,并使用推荐配置。
   - 3.其他的设置，如单引号双引号的选择，占位符的类型等等，可以按照个人喜好来设定。可以参考eslint的官网：  
https://eslint.org/docs/user-guide/configuring
4. 设置快捷键（可选）：  
在`keymap.cson`(可以通过file-keymap打开)里面添加：
  ```
  'atom-text-editor':
    'ctrl-q': 'linter-eslint:fix-file'
  ```
这样ctrl+q后会自动修复可以修复的不符合设定的代码。    
以及使用ctrl+alt+f（默认）调用prettier，美化代码格式。
