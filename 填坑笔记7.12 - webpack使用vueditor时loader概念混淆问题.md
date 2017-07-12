### 文档范例：(未使用webpack进行打包)

```javascript
Vue.use(Vueditor, {
      toolbar: [
        'removeFormat', 'undo', '|', 'elements', 'fontName', 'fontSize', 'foreColor', 'backColor', 'divider', 'bold', 'italic', 'underline', 'strikeThrough',
        'links', 'divider', 'subscript', 'superscript', 'divider', 'justifyLeft', 'justifyCenter', 'justifyRight', 'justifyFull',
        '|', 'indent', 'outdent', 'insertOrderedList', 'insertUnorderedList', '|', 'emoji', 'picture', 'tables', '|', 'switchView'
      ],
      fontName: [
        {val: "arial black"}, {val: "times new roman"}, {val: "Courier New"}
      ],
      fontSize: ['0.8rem', '1.0rem', '1.2rem', '1.5rem', '2.0rem'],
      emoji: [
        "1f600", "1f601", "1f602", "1f923", "1f603", "1f604", "1f605", "1f606"
      ],
      lang: 'en',
      mode: 'iframe',
      iframePath: './dist/iframe/page.html',
      fileuploadUrl: ''
    });
```
iframePath: './dist/iframe/page.html'会正常按路径加载文件

### 我的坑
我在webpack中企图做配置时以url形式引入page.html，但是悲催的是file-loader并没有对html做加载处理，因此我需要将文件加载进来，因为是内存是虚拟的，是找不到文件的，必须通过require import形式加载资源

```javascript

// main.js

let config = {
  toolbar: [
    'removeFormat', 'undo', '|', 'elements', 'fontName', 'fontSize', 'foreColor', 'backColor', 'divider',
    'bold', 'italic', 'underline', 'strikeThrough', 'links', 'divider', 'subscript', 'superscript',
    'divider', 'justifyLeft', 'justifyCenter', 'justifyRight', 'justifyFull', '|', 'indent', 'outdent',
    'insertOrderedList', 'insertUnorderedList', '|', 'emoji', 'picture', 'tables', '|', 'switchView'
  ],
  fontName: [
    { val: "宋体, SimSun", abbr: "宋体" }, { val: "黑体, SimHei", abbr: "黑体" },
    { val: "楷体, SimKai", abbr: "楷体" }, { val: "微软雅黑, 'Microsoft YaHei'", abbr: "微软雅黑" },
    { val: "arial black" }, { val: "times new roman" }, { val: "Courier New" }
  ],
  fontSize: [
    '12px', '14px', '16px', '18px', '20px', '24px', '28px', '32px', '36px'
  ],
  emoji: [
    "1f600", "1f601", "1f602", "1f923", "1f603", "1f604", "1f605", "1f606", "1f609", "1f60a", "1f60b",
    "1f60e", "1f60d", "1f618", "1f617", "1f619", "1f61a", "263a", "1f642", "1f917", "1f914", "1f610",
    "1f611", "1f636", "1f644", "1f60f", "1f623", "1f625", "1f62e", "1f910", "1f62f", "1f62a", "1f62b",
    "1f634", "1f60c", "1f913", "1f61b", "1f61c", "1f61d", "1f924", "1f612", "1f613", "1f614", "1f615",
    "1f643", "1f911", "1f632", "2639", "1f641", "1f616", "1f61e", "1f61f", "1f624", "1f622", "1f62d",
    "1f626", "1f627", "1f628", "1f629", "1f62c", "1f630", "1f631", "1f633", "1f635", "1f621", "1f620",
    "1f607", "1f920", "1f921", "1f925", "1f637", "1f912", "1f915", "1f922", "1f927"
  ],
  lang: 'cn',
  mode: 'iframe',
  iframePath: '/page.html',  // 在这里我是以文件绝对url的形式进行了加载，所以很惨404
  fileuploadUrl: '',
  id: '',
  classList: []
}

```

#### 文档： [救星：file-loader](https://doc.webpack-china.org/loaders/file-loader/)

### 解决问题

1. 引入file-loader
```javascript
	npm install --save-dev file-loader
```   

2. 按文档在main.js中添加loader
```javascript
	require('file-loader?name=page.html!./dist/iframe/page.html')
```   

3. 修改代码，观察run build 
```javascript
	iframePath: '/page.html'
```
按范例做事
```javascript
require("file-loader?name=js/[hash].script.[ext]!./javascript.js");
// => js/0dcbbaa701328a3c262cfd45869e351f.script.js

require("file-loader?name=html-[hash:6].html!./page.html");
// => html-109fa8.html

require("file-loader?name=[hash]!./flash.txt");
// => c31e9820c001c9c4a86bce33ce43b679

require("file-loader?name=[sha512:hash:base64:7].[ext]!./image.png");
// => gdyb21L.png
// 使用 sha512 哈希值替代 md5 并且使用 7 个字符 的 base64

require("file-loader?name=img-[sha512:hash:base64:7].[ext]!./image.jpg");
// => img-VqzT5ZC.jpg
// 使用自定义名称，sha512 哈希值替代 md5 并且使用 base64 的 7 个字符

require("file-loader?name=picture.png!./myself.png");
// => picture.png

require("file-loader?name=[path][name].[ext]?[hash]!./dir/file.png")
// => dir/file.png?e43b20c069c4a01867c31e98cbce33c9
```

你可以使用查询参数 name 为你的文件配置自定义的文件名模板。例如，从你的 context 目录复制文件到输出目录，并且保留完整的目录结构，你可以使用 ?name=[path][name].[ext] 。

默认情况下，会按照你指定的路径和文件名输出文件，且使用相同的 URL 路径来访问文件。

你可以使用 outputPath, publicPath 和 publicPath 查询名称参数，来指定自定义的输出路径和发布目录。

**问号后：Target，感叹号后：Source**

### 启示

加强对webpack文档阅读，积累经验！

