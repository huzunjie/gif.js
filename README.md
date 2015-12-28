
# gif.js

一个用JavaScript实现的GIF编码库,可用于直接在中浏览器生成GIF图片。

基于typed arrays（Uint8Array）和 webWorkers 渲染每一帧，运行起来很快！

**官方示例** - http://jnordberg.github.io/gif.js/

要使用gif.js，必须保证所在环境支持: [WebWorkers - JS子进程](http://www.w3.org/TR/workers/), [File API - Blob](http://www.w3.org/TR/FileAPI/) 和 [Typed Arrays - 二进制数据处理](http://www.cnblogs.com/iicx/p/3859969.html)

官方之前测试过的环境们：
  * Google Chrome
  * Firefox 17
  * Safari 6
  * Internet Explorer 10
  * Mobile Safari iOS 6

## 使用方法

建议将`dist/`目录下的文件放置在项目目录中，将`gif.js`引用到要使用她的页面。（同时保证 `gif.worker.js`在gif.js相同的目录位置。）

代码示例：

```javascript

// 实例化一个GIF对象
var gif = new GIF({
  workers: 2,
  quality: 10
});

// 通过img元素对象来创建帧
gif.addFrame(imageElement);

// 通过canvas元素对象创建帧
gif.addFrame(canvasElement, {delay: 200});

// 通过canvas上下文对象创建帧
gif.addFrame(ctx, {copy: true});

// 通过video当前画面创建帧
gif.addFrame(videoElement, {copy: true});

// GIF生成完毕后通过异步事件监听做相应处理
gif.on('finished', function(blob) {
  window.open(URL.createObjectURL(blob));
});

// 渲染GIF图
gif.render();
```

## GIF类配置项 Options 

Options 可以直接传给构造方法，也可以在实例化之后通过 `setOptions` 方法去设置。

| 配置项key    | 默认值          | 说明                                               |
| -------------|-----------------|----------------------------------------------------|
| repeat       | `0`             | 循环播放次数, `-1` = 不循环播放, `0` = 一直循环    |
| quality      | `10`            | 像素采样间隔, 越低越好                             |
| workers      | `2`             | 用于图像计算处理的JS子进程数                       |
| workerScript | `gif.worker.js` | 用于指webWorker脚本来源URL                         |
| background   | `#fff`          | 当原图是镂空透明图时候用于设定背景色               |
| width        | `null`          | 输出图像的宽度                                     |
| height       | `null`          | 输出图像的高度                                     |
| transparent  | `null`          | transparent hex color, `0x00FF00` = green          |

如果没有通过width\height设置GIF输出时的宽高，将自动从第一帧图像尺寸获取。

### 添加帧（addFrame）方法的配置项(options)

| 配置项key    | 默认值          | 说明                                               |
| -------------|-----------------|----------------------------------------------------|
| delay        | `500`           | 帧延迟的毫秒时长值                                 |
| copy         | `false`         | 复制像素数据                                       |

## 愿景

如果你想多gif.js做一些贡献，下面几个方向都可以去搞一搞。

 * 测试
 * 降级兼容低版本浏览器的研究
 * 抖动显示

## 致谢

gif.js 的参考文献:

 * [Kevin Weiner's Animated gif encoder classes - 凯文·维纳的GIF动画编码器类](http://www.fmsware.com/stuff/gif.html)
 * [Neural-Net color quantization algorithm by Anthony Dekker - 安东尼·德克尔的神经网络颜色量化算法](http://members.ozemail.com.au/~dekker/NEUQUANT.HTML)
 * [Thibault Imbert's as3gif - 迪波因贝特的AS3GIF](https://code.google.com/p/as3gif/)

## 版权许可声明

The MIT License (MIT)

Copyright (c) 2013 Johan Nordberg

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
