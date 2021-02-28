<template>
  <div class="drag" ref="dragger">
    <div
      v-for="(item,index) in dragList"
      :key="item.id"
      class="drag-item"
    >
    <div class="drag_id">
      {{index+1}}
    </div>
    <div class="drag_txt">
      {{ item.name }}
    </div>
    <div class="imgIcon">
    </div>
    </div>
  </div>
</template>

<script>
import Sortable from "sortablejs";
export default {
  name: "Drag",
  data() {
    return {
      dragList: [
        {
          name: "选项A",
          id: 0,
        },
        {
          name: "选项B",
          id: 1,
        },
        {
          name: "选项C",
          id: 2,
        },
        {
          name: "选项D",
          id: 3,
        },
      ],
      seletedId: -1,
     // imgUrl: require("../img/上下.png")
    };
  },
  mounted() {
    this.rowDrop();
  },
  methods: {
    // 图片拖动排序
    rowDrop() {
      const dragList = this.$refs.dragger;
      const that = this;
      Sortable.create(dragList, {
        onEnd({ newIndex, oldIndex }) {
          if (that.dragList.length < 0) return;
          that.dragList.splice(
            newIndex,
            0,
            that.dragList.splice(oldIndex, 1)[0] //先把选中的项删掉, 然后再插入到新的位置
          );
          let newArray = that.dragList.slice(0),
            id = that.dragList[newIndex].id;
          that.dragList = [];
          that.$nextTick(function () {
            that.dragList = newArray;
            that.seletedId = id;
            console.log(that.dragList.map((item) => item.name));
          });
        },
        animation: 150,
        chosenClass: "sortable-chosen",
      });
    },
  },
};
</script>

<style scoped>
.drag-item {
  width: 300px;
  height: 50px;
  line-height: 50px;
  margin: auto;
  position: relative;
  background: #fff;
  display: flex;
  flex-direction: row;
  border-bottom: 1px #010101 solid;

 
}

.drag-item:first-child{
  border-top: 1px #010101 solid;
}
.drag_id {
  width: 50px;
}
.drag_txt{
  width: 200px;
}

.imgIcon{
 width: 45px;
  height: 45px;
}

.sortable-chosen {
  background:#6cf;
  color: #000;
  background-image: url('../img/上下.png');
  background-repeat: no-repeat;
  background-position:260px;
  background-size: 15px;
}
</style>