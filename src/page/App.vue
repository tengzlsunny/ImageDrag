<template>
  <div class="apps">
    <div class="zongZiType">
      <ul class="zongZiTypeUl">
        <li>
            <div class="operating-plat">
              <div class="draggable-node draggable-img1 draggable-img"></div>
            </div>
            <div class="operating-btn">蜜枣</div>
        </li>
        <li>
            <div class="operating-plat">
              <div class="draggable-node draggable-img2 draggable-img"></div>
            </div>
            <div class="operating-btn">豆沙</div>
        </li>
        <li>
            <div class="operating-plat">
              <div class="draggable-node draggable-img3 draggable-img"></div>
            </div>
            <div class="operating-btn">鲜肉</div>
        </li>
      </ul>
    </div>
    <div class="zongZiMainImg">
      <div class="operated droppable-box">
        <div class="operated-con">
          <img src="../assets/img/dragon/food_03.png" alt="" v-if = "food == 1">
          <img src="../assets/img/dragon/food_11.png" alt="" v-if = "food == 2">
          <img src="../assets/img/dragon/food_07.png" alt="" v-if = "food == 3">
        </div>
      </div>
      <img src="../assets/img/dragon/粽子主图.png" alt="">
    </div>
  </div>
</template>

<script>

import './app.css'
import { Drag, Drop } from 'dnd.js'

export default {
  data: _ => ({
    exclusion: '', //三个拖拽互斥，防止拖拽多个卡顿
    food: 0
  }),
  mounted () {
    let that = this
   
    that.dealImg()
  },

  methods:{
    
    // 图片处理
    dealImg () {
      //拖拽
      var _this = this;
      
      // draggableNodes 拖拽元素 Drag
      var draggableNodes = document.querySelectorAll('.draggable-node');
      for (var i = 0; i < draggableNodes.length; i++) {
          new Drag(draggableNodes[i], {
            data: i + 1,
              onDragStart (params) { // 拖拽开始
                _this.exclusion = 1;
                  params.methods.hideStateIcon()
            },
            onDragEnd: function (params) { // 拖拽结束
                
                _this.exclusion = 0;
                !params.target && params.methods.removeDragedNode('back')
            }
          })
      }
        /**
          * 放入重新创建可拖拽元素
          * @param  {[type]} element [description]
          * @return {[type]}         [description]
      */
      function createNewDrap (element) {
          new Drag(element, {
          onDragEnd: function (params) {
              params.methods.removeDragedNode('back')
              var parent = params.el.parentElement
              parent.removeChild(params.el)
          }
          })
      }

      new Drop('.zongZiMainImg', {
          onDrop: function (params) {
               params.methods.removeDragedNode('fade')
              var newNode = params.sourceNode.cloneNode(true)
              createNewDrap(newNode);
              // params data为 draggableNodes中的序号；
              _this.food = params.data;
          }
      })
    }
  }
}
</script>
