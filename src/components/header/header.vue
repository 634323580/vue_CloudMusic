<template>
    <div class="header">
        <div class="menu-btn" @click="nightToggle()">
            <i v-if='nToggle' class="iconfont">&#xe690;</i>
            <i v-else class="iconfont">&#xe6fd;</i>
        </div>
        <ul class="header-nav">
            <router-link v-for="(navList, key) in nav" :key="key" class="list iconfont" v-html="navList.icon" :to="{path: navList.path}" tag="li"></router-link>
        </ul>
        <router-link class="search-btn" tag="div" :to="{path: '/search'}">
            <i class="iconfont">&#xe610;</i>
        </router-link>
    </div>
</template>
<script>
import Bus from '@/common/js/bus'
export default {
  name: 'MyHeader',
  data () {
    return {
        nav: [
            {
                path: '/ranking',
                icon: '&#xe661;'
            },
            {
                path: '/music',
                icon: '&#xe655;'
            }
        ],
        nToggle: this.$store.state.night
    }
  },
  methods: {
      search() {
        Bus.$emit('toggle')
      },
      nightToggle() {
          this.$store.commit('nightToggle')
          this.nToggle = this.$store.state.night
          localStorage.night = this.nToggle
      }
  }
}
</script>
<style lang="scss" scoped>
@import '../../common/scss/var.scss';
.header{
    position:fixed;
    top:0;
    left:0;
    right:0;
    line-height:55px;
    color:#f5f5f5;
    background-color:$dayTheme;
    @extend %padding;
    display: flex;
    justify-content: space-between;
    z-index:10;
    .header-nav{
        display:flex;
        flex:0 0 100px;
        text-align:center;
        .list{
            flex:1;
            color:#e3908f;
            &.on{
                color:#f5f5f5;
            }
        }
    }
    .iconfont{
        font-size:25px;
        display:block;
    }
}
</style>
