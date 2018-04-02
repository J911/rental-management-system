<template>
  <div id="app">
    <div class="header">
      <span>
        <i class="fa fa-archive" aria-hidden="true"></i>

        <span>RMS</span>
      </span>
    </div>
    <div class="ui fluid icon input">
      <input type="text" placeholder="Search...">
      <i @click="toggleModal" class="circular qrcode link icon"></i>
    </div>
    <div class="ui middle aligned divided list">
      <div class="item" v-for="item in items">
        <div class="right floated content">
          <div :class="item.rented == true ? 'ui button' : 'ui button positive'"> {{ item.state }} </div>
        </div>
        <i class="circular archive link icon"></i>
        <div class="content">
          {{ item.name }}
        </div>
      </div>
    </div>
    <div class="modal" v-if="modal">
      <h1>대여하기</h1>
      <qrcode-reader :constraints="constraints" :paused="paused" @decode="onDecode" @locate="onLocate"></qrcode-reader>
      <div class="ui fluid labeled input margin-top">
        <div class="ui label">
           대여자
        </div>
        <input type="text" placeholder="김다른">
      </div>
      <div class="ui two buttons margin-top">
          <div class="ui button active">정보보기</div>
          <div class="ui button">대여하기</div>
      </div>
      <button @click="toggleModal" class="ui fluid red button cancel-btn">
        취소하기
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      items: [
        {
          idx: 1,
          name: "안드로이드 태블릿",
          state: "대여 불가",
          rented: true
        },
        {
          idx: 2,
          name: "가습기",
          state: "대여 가능",
          rented: false
        }
      ],
      constraints: {
        audio: false, // don't request audio stream
        video: {
          facingMode: { ideal: 'environment' }, // use rear camera if available
          width: { max: 1920 }, // constrain video width resolution
        },
      },
      paused: false,
      modal:false
    }
  },
  methods: {
    toggleModal: function(){
      this.modal = !this.modal
    },
    onDecode (content) {
      
    },

    onLocate (points) {
      // ...
    }
  }
}
</script>

<style>
#app {
  color: #2c3e50;
}
.header {
  text-align: center;

  line-height: 80px;
  width: 100%;
  height: 80px;
  background-color: #495057;
  color: white;
  font-size: 2rem;
}
.modal{
  padding: 20px;
  text-align: center;
  color: white;
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  background-color: rgba(0,0,0,0.9);
}
.margin-top{
  margin-top: 10px !important;
}
.modal .cancel-btn{
  margin-top: 40px;
}
</style>
