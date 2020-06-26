**uni-app 自定义进度条、滑动条组件**

![效果图](https://vkceyugu.cdn.bspapp.com/VKCEYUGU-static/a700bd90-b7a2-11ea-b244-a9f5e5565f30.gif)
+ 属性

    |参数|默认值|类型|说明|
    |:---|:---|:---|:---|
    |value|0|Number|设置进度条主进度的值，如50，通过动态设置该值实现进度条进度变化。|
	|subValue|0|Number|设置进度条副进度的值|
	|max|100|Number|最大值，主进度和副进度共用|
    |min|0|Number|最小值，主进度和副进度共用|
	|backgroundColor|rgba(0,0,0,0)|String|组件背景色|
    |activeColor|#0000ff|String|主进度条已经过区域颜色|
	|subActiveColor|#ffaaaa|String|副进度条已经过区域颜色|
    |noActiveColor|#00ffff|String|未经过区域颜色|
    |strokeWidth|30px|String|进度条线宽度|
    |width|300px|String|组件总宽，如果进度值显示在左右两边，则包括进度值在内的宽度|
    |showInfo|true|Boolean|是否显示进度值|
    |infoEndText||String|进度值显示后缀，在原有数字进度的基础上，在其后添加字符|
    |infoFontSize|16px|String|进度值字体尺寸|
    |infoColor|#000000|String|进度值字体颜色|
	|infoContent|value|String|进度值显示主进度值还是副进度值，有效值value、subValue|
    |infoAlign|right|String|进度显示位置，有效值 right center left handle, direction为vertical时，进度值只能显示在handle中|
	|barBorderRadius|5px|String|进度条圆角半径，**注意**：NVUE由于父元素设置为圆角后，被切割的圆角部分子元素无法被隐藏，因此NVUE在使用时，建议不要使用圆角，或者将isActiveCircular设置为true，使子元素也设置为同半径的圆角，但是当进度值较小时，仍会有部分溢出|
    |borderRadius|5px|String|整个组件的border-radius|
	|isActiveCircular|NVUE:true,其他:false|Boolean|主进度和副进度是否为圆角样式，半径为barBorderRadius的值|
    |handleColor|#ffff00|String|拖柄颜色|
    |handleWidth|50px|String|拖柄宽度|
	|handleHeight|40px|String|拖柄高度|
    |handleBorderRadius|5px|String|拖柄圆角半径|
    |handleImgUrl||String|拖柄图片|
    |disabled|false|Boolean|是否禁止拖动|
    |direction|horizontal|String|进度条方向，horizontal or vertical, 注意：设置为vertical时，infoAlign只能设置为handle才有效|
    |step|1|Number|主进度步长，可以为小数，它将决定进度值所保留的小数位数，步长有多少位有效小数（末尾为0不计），进度值就最多保留几位小数，**注意：**step将影响min和max值，如 min=0.1, step=1, 那么最小值会是0；如 min=0.1, step=0.5, max=10,那么进度的最大值会是10.1（四舍五入，max=9.8,此时最大值只能到9.6）,并且可能造成进度条达不到最大值就不能滑动的情况，因此若要完全从设置的min值变化到max,步长应该被max-min整除|
	|subStep|1|Number|副进度步长|
	|continuous|true|Boolean|主进度进度条是否连续滑动，true连续滑动，false步进，即以step的间隔变化|
	|subContinuous|true|Boolean|副进度进度条是否连续滑动，true连续滑动，false步进，即以step的间隔变化|
	|reverse|false|Boolean|进度是否反转，为false时，进度条从左向右滑动，进度值向max靠近，为true时，向min靠近|
    
        
+ 事件

    |事件|返回参数|说明|
    |:---:|:---:|:---:|
    |change|type:change, value:主进度值, sunValue: 副进度值|进度条进度变化触发|
	|valuechange|type:change, value:主进度值, sunValue: 副进度值|主进度条进度变化触发，同时会触发change|
	|subvaluechange|type:change, value:主进度值, sunValue: 副进度值|副进度条进度变化触发，同时会触发change|
    |dragstart|type:dragstart, value:主进度值, sunValue: 副进度值|手指接触进度条触发|
    |dragging|type:dragging, value:主进度值, sunValue: 副进度值|拖拽进度条触发|
    |dragend|type:dragend, value:主进度值, sunValue: 副进度值|拖拽完成手指离开屏幕触发|

