<template>
    <div class='container'>
        <web-view :src="url"></web-view>
    </div>
</template>

<script>
export default {
  components: {
  
  },
   data() {
    return {
        url:'',
    };
  },
  created() {
    //   this.url = localStorage.getItem('urldetail');;
  },
  onShow () { //必须是在onLoad钩子函数往后的生命周期中获取
    this.url = this.$root.$mp.query.url;
},
  mounted() {
    // wx.showLoading({
    //     title: "加载中"
    //   });
  },
  computed: {},

  methods: {},
 
};
</script>

<style lang='scss' scoped>
.container {
  height: 100vh;
  background-color: rgb(245, 245, 239);
}
</style>
