# 使用ATOM编辑器进行babel(ES6/ES7)，React开发的插件配置

## 写在前面
这是本专栏/公众号/简书的第一篇文章，所以也就打算写一篇比较“像是第一篇文章”的文章。
虽然说是第一次，但是如果您初次接触web开发，那么我并不推荐您使用ATOM, VS Code这类可以高度自定义的编辑器。如果您正在熟悉基础的HTML+CSS & JavaScript，WebStorm应该是您最好的选择。

## 概览
1. 插件安装
2. 插件配置
3. 填坑

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
1. 在全局安装eslint, eslint-plugin-react, babel-eslint(您也可以使用每个project内部的这些包，一般可以全局安装)
运行： `npm install -g eslint eslint-plugin-react babel-eslint`
