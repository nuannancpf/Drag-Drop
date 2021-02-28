<template>
  <div id="app">
    <!-- <Drag></Drag> -->
  </div>
</template>

<script>
import Drag from '@/components/Drag.vue'
export default {
  data() {
    return {
      msg: "这是测试组件",
      colors: [
        {
          id: 1,
          text: '选项A'
        },
        {
          id: 2,
          text: '选项B'
        },
        {
          id: 3,
          text: '选项C'
        },
        {
          id: 4,
          text: '选项D'
        },
      ],
      startArr: [],
      endArr: [],
      count: 0,
      clickIndex: 0,
    };
  },
  methods: {
    getdata(evt) {
      console.log(evt.draggedContext.item.text);
    },
    datadragEnd(evt) {
      evt.preventDefault();
      this.clickIndex = evt.oldIndex
      console.log('选择',evt)
     this.clickColor(evt.id)
      console.log("拖动前的索引 :" + evt.oldIndex);
      console.log("拖动后的索引 :" + evt.newIndex);
      console.log(this.colors);
    },
    clickColor(id){
      // evt.preventDefault();
      console.log('选中改变颜色', id)
      this.clickIndex = id
    }
  },
  mounted() {
    //为了防止火狐浏览器拖拽的时候以新标签打开，此代码真实有效
    document.body.ondrop = function (event) {
      event.preventDefault();
      event.stopPropagation();
    };
  },
  components: {
    draggable,
    Drag
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.test {
  border: 1px solid #ccc;
}
.drag-item {
  width: 200px;
  height: 50px;
  line-height: 50px;
  margin: auto;
  position: relative;
  background: #ddd;
  margin-top: 20px;
  display: flex;
  flex-direction: row;
 
}
.red{
  background-color: green;
}
.drag_id{
  width: 50px;
}
.ghostClass {
  opacity: 1;
}
.bottom {
  width: 200px;
  height: 50px;
  position: relative;
  background: blue;
  top: 2px;
  left: 2px;
  transition: all 0.5s linear;
}
</style>
