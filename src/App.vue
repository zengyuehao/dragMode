<template>

  <div id="app">
    <div class="box">
      <img v-for="(item,i) in dataList" :key="item.id" :data-index="i"
      :src="item.src" alt="" @dragstart="handleDragStart" @dragend="handleDragEnd" @mousedown="handleMouseDown">
    </div>
    <div class="show" @dragenter="handleDragEnter" @dragover="handleDragOver"  @drop="handleDrop">

    </div>
  </div>

</template>

<script>
export default {
  data() {
    return {
      startX: 0,
      StartY: 0,
      offsetX: 0,
      offsetY: 0,
      dataList: [
        {
          id: 1,
          src: '/img/1.b623f260.jpeg'
        },
        {
          id: 2,
          src: '/img/2.49d6d486.jpeg'
        }
      ]
    }
  },
  methods: {
    handleDragStart(e){
      console.log(e);
      var idx = e.target.dataset.index
      console.log(parseInt(idx));
      var img = document.querySelectorAll('img')[parseInt(idx)]
      console.log(img);
      this.offsetX = img.offsetLeft
      this.offsetY = img.offsetTop
      e.dataTransfer.setData('text',img.src)
    },
    handleDrop(e){
      var mysrc = e.dataTransfer.getData('text')
      var myimg = document.createElement('img')
      var d2 = document.querySelector('.show')
      myimg.src = mysrc
      myimg.style.position = 'absolute'
      myimg.width = '100'
      myimg.style.left = e.offsetX - this.startX + this.offsetX + 'px'
      myimg.style.top = e.offsetY - this.StartY + this.offsetY + 'px'
      d2.appendChild(myimg)
    },
    handleDragEnd(e) {
      

      this.chaX = Math.abs(this.startX - this.EndX)
      this.chaY = Math.abs(this.StartY - this.EndY )


    
    },
    handleDragOver(e) {
      e.preventDefault();
      
    },
    handleDragEnter(e) {

      e.preventDefault();
    },
    handleMouseDown(e) {
      var cilentLeft  = document.documentElement.cilentLeft;
      console.log(cilentLeft);
      this.startX = e.clientX
      this.StartY = e.clientY
      console.log(this.startX);
    }
  }
}  
</script>


<style lang="less">
  img {
    position: relative;
    top: 0;
    left: 0;
    width: 100px;
    height: 100px;
  }
  .box {
    height: 100vh;
    widows: 200px;
    float: left;
  }
  .show {
    position: relative;
    background-color: red;
    width: 1000px;
    height: 100vh;
    float: right;
  }
</style>
