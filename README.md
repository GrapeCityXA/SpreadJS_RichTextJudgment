# SpreadJS_RichTextJudgment
判断当前单元格是否为富文本
### SpreadJS 示例，基于 JavaScript组件实现富文本格式判断

该示例包括使用 SpreadJS API 的演示脚本，可用于实现包含合并单元格的数据绑定。
有关 SpreadJS API 的更多信息，请参阅[SpreadJS API指南]( https://demo.grapecity.com.cn/spreadjs/help/api/) 和[帮助手册]( https://help.grapecity.com.cn/pages/viewpage.action?pageId=5963808)。
 

目录：
-	运行步骤
-	控件初始化
-	示例代码
-	关于 SpreadJS
外部文件：
-	临时授权申请



### 运行步骤
1、在开始之前，请确保您已满足以下先决条件：

要运行 SpreadJS，浏览器必须支持 HTML5，客户端导入和导出 Excel 需要 IE10及以上。请先了解 [SpreadJS 的产品使用环境]( https://www.grapecity.com.cn/developer/spreadjs/selection-guide/product-use-environment)，并申请临时部署授权激活
安装并更新NodeJS和NPM
2、克隆或下载此代码库
3、初始化控件，并运行示例脚本

#### 控件初始化
1、	首先，创建一个新页面，并在页面上输入以下代码：
```
<!DOCTYPE html>
    <html>
    <head>
        <title>Spread HTML test page</title>
```
2、在页面中添加对 Spread.JS 的引用。代码如下。需要注意的是，Spread 提供压缩过
```
（minified）的 JavaScript 文件和和用于调试的文件：
<script src="[Your_Scripts_Path]/gc.spread.sheets.all.xxxx.min.js" type="text/javascript"></script>
```

3、添加 CSS 文件以改变Spread.JS 的外观。默认的CSS文件名为： 
gc.spread.sheets.xxxx.css，里面包含了所有的默认样式。该 CSS 文件将会影响滚动条，筛选框及其子元素，单元格和下方标签栏的样式。引入 CSS 的代码如下：

```
//<link href="[Your_CSS_Path]/gc.spread.sheets.xxxx.css" rel="stylesheet" type="text/css"/>
//OR
<link href="[Your_CSS_Path]/bootstrap/bootstrap.min.css" rel="stylesheet" type="text/css"/>
<link href="[Your_CSS_Path]/bootstrap/bootstrap-theme.min.css" rel="stylesheet" type="text/css"/>
```
4、添加产品授权，代码为：
```
GC.Spread.Sheets.LicenseKey = "xxx";
```
5. 添加控件初始化代码。本例会在一个 id 为“ss”的 DOM 元素上初始化 Spread.Sheets：
```
<script type="text/javascript">
// Add your license
 GC.Spread.Sheets.LicenseKey = "xxx";
// Add your code
 window.onload = function(){
var spread = new GC.Spread.Sheets.Workbook(document.getElementById("ss"),{sheetCount:3});
var sheet = spread.getActiveSheet();
 }
</script>
</head>
<body>
```
6、 创建一个 id 为 “ss”的元素，Spread.Sheets 将在该 DOM 中初始化：
```
<div id="ss" style="height: 500px; width: 800px"></div>
</body>
</html>
```
#### 示例代码
```
HTML：
    <div id='log'></div>
    <p>判断当前单元格是否为富文本格式</p>
    <div id='ss'></div>
CSS：
    #ss{height:400px;width:100%}
    p{
        text-align: #336699;
        color: red;
    }
JavaScript：
    GC.Spread.Common.CultureManager.culture('zh-cn');
    var spread = new GC.Spread.Sheets.Workbook(document.getElementById('ss'))
    var sheet = spread.sheets[0]
    sheet.setValue(0,2,{richText:[{style:{font:'bold 12px Arial'},text:'SpreadJS'}]}, GC.Spread.Sheets.SheetArea.viewport);
        sheet.setValue(1,2,{richText:[{style:{font:'bold 12px Arial'},text:'javascript'}]}, GC.Spread.Sheets.SheetArea.viewport);
        sheet.setValue(2,2,{richText:[{style:{font:'bold 12px Arial'},text:'css'}]}, GC.Spread.Sheets.SheetArea.viewport);
        sheet.setValue(3,2,'hello')
    
    sheet.bind(GC.Spread.Sheets.Events.CellDoubleClick, function(sender, args) {
        var col = args.col;
        var row = args.row;
        var rich = sheet.getValue(row,col,GC.Spread.Sheets.SheetArea.viewport, GC.Spread.Sheets.ValueType.richText);
        if (rich.richText) {
            if (rich.richText.length > 0) {
                alert('富文本')
            }
            return
        }else{
            alert('非富文本')
        }
})
```
#### 关于 SpreadJS
[SpreadJS]( https://www.grapecity.com.cn/developer/spreadjs) 是一款基于 HTML5 的纯前端表格控件，兼容 450 多种 Excel 公式，具备“高性能、跨平台、与 Excel 高度兼容”的产品特性。使用 SpreadJS，可直接在 Angular、 React、 Vue 等前端框架中实现高效的模板设计、在线编辑和数据绑定等功能，为最终用户提供高度类似 Excel 的使用体验。
 

