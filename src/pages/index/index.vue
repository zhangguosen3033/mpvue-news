<template>
    <div class='container'>
        <div class='header'>

            <scroll-view class="scroll-view_x" scroll-x style="width: auto;overflow:hidden;" scroll-with-animation="true">
                <div class="item" :class="[selectTab == index ? 'activeItem' : 'item']" v-for='(headItem,index) in headTitle' :key='index' @click="tabSelct(headItem,index)">{{headItem}}</div>
            </scroll-view>
        </div>

        <div class="card">
            <card :items="dataList"></card>
        </div>

        <div class="noData">没有更多了，看看其他版块吧</div>
    </div>
</template>

<script>
import card from "@/components/card";
export default {
  data() {
    return {
      headTitle: [
        "头条",
        "社会",
        "国内",
        "国际",
        "娱乐",
        "体育",
        "军事",
        "科技",
        "财经",
        "时尚"
      ],
      selectTab: "0",
      dataList: [],
      imageArr: []
    };
  },
  components: {
    card
  },
  computed: {
   
  },
  watch: {},
  created() {
      wx.showLoading({
        title: "加载中"
      });
    this.$http
      .get("http://toutiao-ali.juheapi.com/toutiao/index", {})
      .then(d => {
        this.dataList = d.data.result.data;
        wx.hideLoading();
      })
      .catch(e => console.log("error", e));
  },
  async onPullDownRefresh() {
  // to doing..
  console.log('刷新啊刷新');
   this.tabSelct();

},
  methods: {
    tabSelct(headItem, index) {
      this.selectTab = index;
       wx.showLoading({
        title: "加载中"
      });
      var typeStr;
      switch (index) {
        case 0:
          {
            typeStr = "top";
          }
          break;
        case 1:
          {
            typeStr = "shehui";
          }
          break;
        case 2:
          {
            typeStr = "guonei";
          }
          break;
        case 3:
          {
            typeStr = "guoji";
          }
          break;
        case 4:
          {
            typeStr = "yule";
          }
          break;
        case 5:
          {
            typeStr = "tiyu";
          }
          break;
        case 6:
          {
            typeStr = "junshi";
          }
          break;
        case 7:
          {
            typeStr = "keji";
          }
          break;
        case 8:
          {
            typeStr = "caijing";
          }
          break;
        case 9:
          {
            typeStr = "shishang";
          }
          break;

        default:
          break;
      }

       this.$http
      .get("http://toutiao-ali.juheapi.com/toutiao/index"+ '?type='+typeStr, {})
      .then(d => {
        this.dataList = d.data.result.data;
        wx.hideLoading();
         // 停止下拉刷新
        wx.stopPullDownRefresh();
      })
      .catch(e => console.log("error", e));
        // 停止下拉刷新
        wx.stopPullDownRefresh();
    }
  }
};
</script>

<style lang="scss" scoped>
.container {
  background-color: rgb(245, 245, 249);
  font-size: 30rpx;
  overflow: hidden;
  background: #fff;
  width: 100vw;
  .header {
    position: fixed;
    width: 100%;
    height: 86rpx;
    overflow: hidden;
    white-space: nowrap;
    background-color: #41b883;

    .item {
      width: 150rpx;
      background-color: #41b883;
      color: white;
      text-align: center;
      height: 83rpx;
      line-height: 83rpx;
      display: inline-block;
    }
    .activeItem {
      color: #fe9f28;
      border-bottom: 4rpx #fe9f28 solid;
    }
  }
  .card {
    margin-top: 86rpx;
    width: 100%;
  }
  .noData{
      margin-top: 20rpx;
      text-align: center;
      font-size: 22rpx;
      color: #999;

  }
}
</style>

