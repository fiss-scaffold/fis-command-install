# fiss-command-install

## Usage

    Usage: install <name> [options]

    Options:

      -h, --help         output usage information
      --save             save component(s) dependencies into `components.json` file.
      -r, --repos <url>  repository url

## fiss install在fis3 install基础上的改进
添加了在`component.json`中配置`exclude`项排除文件和目录被安装的功能。`exclude`配置项的语法请参考[globs](https://github.com/isaacs/minimatch#usage)。
### 配置示例：
组件目录：
```
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
.
├── component.json
├── index.js
└── widgets
```
