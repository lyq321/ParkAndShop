<template>
  <div style="width: 1000px; margin: 0px auto;">
    <div style="width: 1000px; min-width: 1000px; margin: 0px auto;">

      <div style="width: 1000px; height: 83px; padding: 0px 0px; margin: 0px auto;">
        <img src="../../assets/logo.png" style="float: left;" height="83px" width='210px'/>
        <p style="float: left; color: rgb(60, 60, 60); line-height: 83px; font-size: 22px; font-weight: 700; margin-left: 20px">Shop</p>
      </div>
      <div style=" width: 1000px;height: 19px; padding: 6px 0px; border-bottom: 2px solid #f40">
        <p style="float: left;font-size: 13px; font-weight: 500; color: rgb(60, 60, 60);">Shop Name:&nbsp;&nbsp; {{ info.shopName }}</p>
        <p style="float:left; text-align:center; margin-left:10px;font-size: 13px; font-weight: 500; color: #fff; width: 70px; height: 19px; border-radius: 3px; background: #f40;">SHOP</p>
      </div>
      <div style="height: 120px; width: 1000px;">
        <img v-bind:src="info.url"
             style="float: left; width: 118px; height: 118px; border: 1px solid rgb(212,215,220)"/>
        <p src="../../assets/logo.png" style="float:left; width: 880px; height: 120px; font-size: 30px; line-height: 120px; text-align: center; color: rgb(63,127,206);">{{ info.shopName }}</p>
      </div>
    </div>
    <router-view/>
    <good v-show="false" v-on:childByValue="childByValue"/>
    <shop v-show="false" v-on:childByValue="childByValue"/>
  </div>
</template>

<script>
import Loading from '@/components/common/Loading'
import Good from '@/components/seller/Good'
import Shop from '@/components/seller/Shop'
export default {
  components: {Loading, Good, Shop},

  data () {
    return {
      id: -1,
      info: {
      }
    }
  },

  methods: {
    childByValue: function (childValue) {
      // childValue就是子组件传过来的值
      if (childValue !== '') {
        this.id = childValue
        this.isLoad = true
        console.log(this.id)
        this.$http.get(this.URL + 'b/info/get?id=' +
          this.id)
          .then((data) => {
            console.log(data)
            this.isLoad = false
            const response = data.body
            this.info = response.data.data
          })
          .catch(() => {
            this.isLoad = false
          })
      }
    }
  }

}
</script>

<style scoped>

  *{
    margin: 0px;
    padding: 0px;
    display: block;
  }

  ul{
    margin: 0px auto;
  }

  li{
    width: 240px;
    margin-top: 10px;
    margin-left: 5px;
    margin-right: 5px;
    height: 322px;
    float: left;
  }

</style>
