# fiss-command-install

## Usage

    Usage: install <name> [options]

    Options:

      -h, --help         output usage information
      --save             save component(s) dependencies into `components.json` file.
      -r, --repos <url>  repository url
      -i, --ignore       ignore excluded path

## fiss install在fis3 install基础上的改进

### 设置默认参数
+ `protocol`: `gitlab`
+ `gitlab`:
  + `author`: `fecom-fe`
  + `domain`: `http://gitlab.58corp.com/`
  + `token`: `********************`

如果执行`fiss install comp`，会默认安装`fecom-fe`下的`comp`组件  
安装其他作者的组件请执行`fiss install other/comp`命令

### 无`component.json`安装组件
可在项目目录中不存在`component.json`文件的情况下安装组件，默认会使用如下配置：
```
{
  "protocol": "gitlab",
  "gitlab": {
    "author": "fecom-fe",
    "domain": "http://gitlab.58corp.com/",
    "token": "...................."
  }
};
```
执行`fiss install component`后组件会被默认安装到项目中的`components`目录

### 定制安装目录
添加了在`component.json`中配置`dir`项来定制安装目录的功能。
+ 配置示例：
```json
{
  "name": "widgets-demo",
  "description": "A demo widget",
  "dir": "dirname",
  "version": "1.0.6",
  "dependencies": [],
  "exclude": []
}
```
执行`fiss install`后组件会被安装到项目中的`dirname`目录。
### 目录排除
添加了在`component.json`中配置`exclude`项排除文件和目录被安装的功能。`exclude`配置项的语法请参考[globs](https://github.com/isaacs/minimatch#usage)。**如果指定了`-i`参数，则不会排除这些文件和目录。**
+ 配置示例： 

组件目录：
```
widgets-demo
├── README.md
├── component.json
├── index.js
├── src
└── widgets
```
`component.json`：
```json
{
  "name": "widgets-demo",
  "description": "A demo widget",
  "version": "1.0.6",
  "dependencies": [],
  "exclude": [
    "src",
    "README.md"
  ]
}
```
那么执行`fiss install`命令后，`src`目录和`README.md`文件不会被安装。
```
widgets-demo
├── component.json
├── index.js
└── widgets
```
