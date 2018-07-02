## 图片拖拽

#### vue依赖注入dnd.js
     npm install --save dnd.js
     * 注入后，node_module的dnd.js的dist文件夹中的dnd.js没有考虑出现滚动轴的定位情况，所以有所修改
     * 如果你的拖拽部分没有出现window的滚动条，则不需要做任何修改
     * 如果你的拖拽部分出现了滚动条，请将node_module的dnd.js文件夹的dist问价夹中的dnd.js替换成根目录下的dnd.js

#### 为避免img标签的默认属性，拖拽的图片尽量设置成背景图（对火狐浏览器的兼容）

#### 拖拽图片设置css样式的时候不要加给这个元素加父元素
     如： .draggable-img 不要写成 .zongZiTypeUl .draggable-img
     * 如果写成.zongZiTypeUl .draggable-img拖拽可能失败