# 记录细节以便整理

## 2018/9/26

- elementui 在使用el-card 或者el-col 或el-row时，要想触发click事件，需要添加修饰符native
  ```html
   <el-row @click.native = open>
        nothing here
   </el-row>
  ```  

- localstorage.name和localstorage.getItem('name')的区别
    - localsorage.getitem('name')是动态取值，所以建议任何时候，优先使用localstorage.getItem()和localstorage.setItem()
  
- firefox 不支持window.event,所以当某个函数执行过程中需要传递参数，而无法直接使用e作为默认参数时。在vue下可以在参数末尾新加一个$event来作为e，在函数中被使用

- vue 无法再点击的时候通过this来获取点击对象，最好的代替方法是使用事件的target对象。e.target对象可以直接获取并操作当前dom元素

- echarts 柱状图超出y轴，原因在于boundaryGap属性，默认为true，改为false后可解决，如果仍然不能解决，则直接注释此属性可以解决

- vue的watch监听中，如果被监听的数据被重新赋值，但是newValue和oldValue值相等，那么不会触发watch事件。解决方法是使用immediate = true 来深度监听.
  ```js
    canEdit:  {
                immediate: true,
                handler: function (val) {
                    console.log(val);
                    this.editCode = (val || localStorage.getItem('isEdit'));
                }
            }
  ```

- 百度地图手绘路线，关于绘图工具的选择
   ```js
   this.drawingManager = new BMapLib.DrawingManager(this.map, {
                    isOpen: false, // 是否开启绘制模式
                    enableDrawingTool: true, // 是否显示工具栏
                    drawingToolOptions: {
                        anchor: BMAP_ANCHOR_TOP_RIGHT,
                        offset: new BMap.Size(0, 0),
                        drawingModes: [BMAP_DRAWING_POLYLINE], //选择开启哪些工具
                    },
                    polylineOptions: styleOptions,
                    enableCalculate: true
                });
    ```

- 禁止输入中文的正则
  - input输入框中使用 oninput事件中监听输入值
  - ``` js
    oninput="this.value=this.value.replace(/[\u4E00-\u9FA5]/g,'');"
    ```

- 过滤器来选择格式化样式
  - ```js
    Vue.filter('truncate', function (text, stop, clamp) {
    if (text) {
        return text.slice(0, stop) + (stop < text.length ? clamp || '...' : '');
        }
    });
    ```