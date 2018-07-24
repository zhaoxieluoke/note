## lodop web打印使用文档  

### 在页面引入lodop打印控件  

> 嵌入  
```
    <script language="javascript" scr="LodopFuncs.js"></script>
    <object id="LODOP" classid="clsid:2105C259-1E0C-4534-8141-A753534CB4CA" width=0 height=0>
        <embed id="LODOP_EM" type="application/x-print-lodop" width=0 height=0></embed>
    <object>
```  
在调用lodop之前, 先使用如下对象获取控件对象  
var LODOP=getLodop(document.getElementById('LODOP_OB'),document.getElementById('LODOP_EM'));  

> 简写方式  
```
    //引入LodopFunc.js 之后 
    //获取控件对象
    var LODOP = getLodop();  
    
```