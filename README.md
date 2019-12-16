# ECharts-Demo
这是微信小程序的echarts示例项目

## 创建第一个ECharts小程序图表
步骤1：在pages文件夹下，创建page文件，命名为`index`，此时在pages文件夹下将会有4个文件，分别为`index.wxml`、`index.wxss`、`index.json`、`index.js`。

步骤2：为了能够在`index.wxml`中使用组件`ec-canvas`,需要在`index.json`进行如下设置

``` json
// index.json
"usingComponents": {
    "ec-canvas": "/components/ec-canvas/ec-canvas" //相对路径和绝对路径皆可
}
```

步骤3：在`index.wxml`中使用`ec-canvas`

```html
<!-- index.wxml -->
<view class="container">
  <ec-canvas id="mychart-dom-bar" canvas-id="mychart-bar"></ec-canvas>
</view>
```

步骤4：在`index.wxss`中为`ec-canvas`设置宽高

```css
/**index.wxss**/
.container {
	width:100%;
	height:100%;
	position: absolute;
	top: 0;
	bottom: 0;
	left: 0;
	right: 0;
} 
```

步骤5: 在`index.js`中，创建ECharts实例，并且初始化图标数据

```js
//index.js
//获取应用实例
// 这里一定是相对路径
import * as echarts from '../../components/ec-canvas/echarts';
let chart = null;
// 2、进行初始化数据
function initChart(canvas, width, height) {
  chart = echarts.init(canvas, null, {
    width: width,
    height: height
  });
  canvas.setChart(chart);
  const option = {
    color: ['#37a2da', '#32c5e9', '#67e0e3'],
    tooltip: {
      trigger: 'axis',
      axisPointer: {            // 坐标轴指示器，坐标轴触发有效
        type: 'shadow'        // 默认为直线，可选为：'line' | 'shadow'
      }
    },
    legend: {
      data: ['热度', '正面', '负面']
    },
    grid: {
      left: 20,
      right: 20,
      bottom: 15,
      top: 40,
      containLabel: true
    },
    xAxis: [
      {
        type: 'value',
        axisLine: {
          lineStyle: {
            color: '#999'
          }
        },
        axisLabel: {
          color: '#666'
        }
      }
    ],
    yAxis: [
      {
        type: 'category',
        axisTick: { show: false },
        data: ['北京百星', '成都溧阳', '百度贴吧', '一点资讯', '微信', '微博', '知乎'],
        axisLine: {
          lineStyle: {
            color: '#999'
          }
        },
        axisLabel: {
          color: '#666'
        }
      }
    ],
    series: [
      {
        name: '热度',
        type: 'bar',
        label: {
          normal: {
            show: true,
            position: 'inside'
          }
        },
        data: [300, 270, 340, 344, 300, 320, 310],
        itemStyle: {
          emphasis: {
            color: '#37a2da'
          }
        }
      },
      {
        name: '正面',
        type: 'bar',
        stack: '总量',
        label: {
          normal: {
            show: true
          }
        },
        data: [120, 102, 141, 174, 190, 250, 220],
        itemStyle: {
          emphasis: {
            color: '#32c5e9'
          }
        }
      },
      {
        name: '负面',
        type: 'bar',
        stack: '总量',
        label: {
          normal: {
            show: true,
            position: 'left'
          }
        },
        data: [-20, -32, -21, -34, -90, -130, -110],
        itemStyle: {
          emphasis: {
            color: '#67e0e3'
          }
        }
      }
    ]
  };
  chart.setOption(option);
  return chart;
}

Page({
  data: {
    ec: {
      onInit: initChart // 3、将数据放入到里面
    }
  }
});
```

步骤6：在`index.wxml`中将数据传入组件`ec-canvas`

```html
<!-- index.wxml -->
<view class="container">
  <ec-canvas id="mychart-dom-bar" canvas-id="mychart-bar" ec="{{ec}}"></ec-canvas>
</view>
```

最后，你所看到的图表


```echarts
var option = {
    color: ['#37a2da', '#32c5e9', '#67e0e3'],
    tooltip: {
      trigger: 'axis',
      axisPointer: {            // 坐标轴指示器，坐标轴触发有效
        type: 'shadow'        // 默认为直线，可选为：'line' | 'shadow'
      }
    },
    legend: {
      data: ['热度', '正面', '负面']
    },
    grid: {
      left: 20,
      right: 20,
      bottom: 15,
      top: 40,
      containLabel: true
    },
    xAxis: [
      {
        type: 'value',
        axisLine: {
          lineStyle: {
            color: '#999'
          }
        },
        axisLabel: {
          color: '#666'
        }
      }
    ],
    yAxis: [
      {
        type: 'category',
        axisTick: { show: false },
        data: ['北京百星', '成都溧阳', '百度贴吧', '一点资讯', '微信', '微博', '知乎'],
        axisLine: {
          lineStyle: {
            color: '#999'
          }
        },
        axisLabel: {
          color: '#666'
        }
      }
    ],
    series: [
      {
        name: '热度',
        type: 'bar',
        label: {
          normal: {
            show: true,
            position: 'inside'
          }
        },
        data: [300, 270, 340, 344, 300, 320, 310],
        itemStyle: {
          emphasis: {
            color: '#37a2da'
          }
        }
      },
      {
        name: '正面',
        type: 'bar',
        stack: '总量',
        label: {
          normal: {
            show: true
          }
        },
        data: [120, 102, 141, 174, 190, 250, 220],
        itemStyle: {
          emphasis: {
            color: '#32c5e9'
          }
        }
      },
      {
        name: '负面',
        type: 'bar',
        stack: '总量',
        label: {
          normal: {
            show: true,
            position: 'left'
          }
        },
        data: [-20, -32, -21, -34, -90, -130, -110],
        itemStyle: {
          emphasis: {
            color: '#67e0e3'
          }
        }
      }
    ]
  };
```
