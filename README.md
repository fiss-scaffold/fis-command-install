# fiss-command-install

## Usage

    Usage: install <name> [options]

    Options:

      -h, --help         output usage information
      --save             save component(s) dependencies into `components.json` file.
      -r, --repos <url>  repository url

## fiss install在fis3 install基础上的改进
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
添加了在`component.json`中配置`exclude`项排除文件和目录被安装的功能。`exclude`配置项的语法请参考[globs](https://github.com/isaacs/minimatch#usage)。
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
