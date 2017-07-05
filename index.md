## Welcome to GitHub Pages
  echarts虽然很好上手，但是我们在使用过程中，不免也会遇到一些让人抓狂的问题，下面这些是我在用的过程中，遇到的问题，或许这只是一点已问题，但是，如果刚好你也遇到了，可以参考一下^-^

### 增加y轴名字以及各种样式 yAxis: {}
```
- 增加名字
  在对象中添加属性     name:'增长速度',
- 增加名字样式
  添加属性 nameTextStyle:{color: '#1e90ff',fontFamily: 'verdana',fontSize: 16, }
- 增加名字与y轴之间的距离
  添加属性：nameGap:40,
- 增加y轴坐标之间的差值
  添加属性 boundaryGap: [0, 0],上和下的
- 名字的位置
  添加属性 position: 'left',（或者center等，可以在api上查看）
- 增加网格以及样式
  添加属性 splitLine:{show: true,lineStyle(网格线条的样式): {color:['red'],width:1,type:'solid'}}

```
### 改变折线图折点的样式
```
- 将折点由空心变成实心
  在series:[{}]数组的对象中增加   symbol:'circle',
```
### 改边图标右上角的切换图标样式
```
http://echarts.baidu.com/option.html#toolbox.iconStyle
首先是toolbox{iconStyle：{normal：{}，emphasis:{}}}
- 改变图标的颜色等
  在normal中写borderWidth:1,borderColor:'white'
- 改变鼠标经过图标的样式
  在emphasis写（别的也是），这个我之前使用的时候没有用到这个属性，那天突然要将鼠标经过圆点出现的小提示变成一个表格，我就去找。找了半天。突然在api上看到这个属性，然后就没想就去试试。结果还真是，然后感觉打开了一片新大陆一样，哈哈

```

### 使用echarts做折线图的时候，想要任意切换折线图、柱状图，返回，下载、导出等，怎么做？
```
   直接在option中设置 toolbox: {
                         feature: {
                         dataZoom: {yAxisIndex: 'none'},
                         dataView: {readOnly: false},
                         magicType: {type: ['line', 'bar']},
                         restore: {},
                         saveAsImage: {}
                }
            }

```
### 使用echarts地图功能的时候，怎么将地图引入
```
   导入jquery（为了之后请求数据使用）、echarts.js、china.js（这是中国地图的js，还有对应的json文件一并获取，其他各省的或者世界地 图的这个网址http://echarts.baidu.com/download-map.html获取）
```

### 使用echarts进行节点操作的时候，怎么进行操作
```
   myChart.on('click', function (params) {
            console.log(params);
        });
```

### 当进行dom操作的时候，阻止冒泡实现不了（event用不了）
```
   在echarts中的event事件和我们平时js中的event不一样，所以要在别处进行原始event的保存，然后在echarts中进行使用

```
### echarts力导图中节点进行更改形状或者大小，或者指定形状怎么做？
```
   使用option -> series -> nodes -> symbolSize: 数值  --->更改节点的大小
      使用option -> series -> nodes -> symbol: 'circle'或者 'rect'或者 'roundRect'或者 'triangle'或者 'diamond'或者 'pin'或者 'arrow' 或
      者'image://url  --->更改节点的形状样式，最后一个是将节点更改成图片；

```

### echarts图怎么能够获取他的某一帧的图片？
```
   首先要有一个canvas的盒子，对canvas盒子进行宽高的设置，以及初始化之后进行放置；
     1）var offcanvas = myChart.getRenderedCanvas({pixelRatio: 1,});
     ctx.drawImage(offcanvas,0,10,1058,800);参数的意思分别是：（img，x，y，width，height）(x,y从这个坐标开始作图)
     截止到这一步，就将某一帧的动画保存到canvas上，之后可以设置定时器或者别的，让这个canvas随时变化
     2）将canvas画布保存成图片（http://www.webhek.com/convert-canvas-image/ ）
         function convertCanvasToImage(canvas,image) {
             srcCan=canvas.toDataURL("image/png");  //获取到图片信息，这里获取到的是图片的base64码
             image.src =srcCan;
             return image;
         }
    3）根据需要执行这个函数，设置判断逻辑
```

### 使用require和angular的时候引用echarts，报错，说明echarts这个服务没有被注入？
```
  这个属于粗心问题，但是对于新手的我，确实找了一会呢
  在app中进行配置服务app.factory('echarts',function(){return echarts;});
  然后要注意的是，要引用3.0以上的echarts的版本，使用低版本的不可，不需要对echarts中进行改变，直接引用就可， 不需要写defined

```
