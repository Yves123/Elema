<template>
  <div>
     <vheader :seller='seller'></vheader>
     <div class="tab border-1px">
       <div class="tab-item"><a v-link="{ path:'/goods'}">商品</a></div>
       <div class="tab-item"><a v-link="{ path:'/ratings'}">评论</a></div>
       <div class="tab-item"><a v-link="{ path:'/seller'}">商家</a></div>
     </div>
     <router-view></router-view>
  </div>
</template>

<script>
    import vheader from './components/header/header'
    const ERR_OK = 0

    export default {
        data() {
                return {
                    seller: {}
                }
            },
            created() {
                this.$http.get('/api/seller').then(function(response) {
                    response = response.body
                    if (response.erron === 0) {
                        this.seller = response.data
                    }
                })
            },
            components: {
                vheader: vheader
            }
    }
</script>

<style lang='stylus' rel='stylesheet/stylus'>
    @import './common/stylus/index.styl' 
    .tab {
        display: flex ;
        width: 100%;
        height: 40px;
        line-height: 40px;
        border-1px(rgba(7, 17, 27, 0.1))
    }
    
    .tab .tab-item {
        flex: 1;
        text-align: center
    }
    
    .tab .tab-item a {
        display: block;
        text-decoration: none;
        font-size: 14x;
        color: rbg(77, 85, 93)
    }
    
    .tab .tab-item a.active {
        color: rgb(240, 20, 20)
    }
</style>