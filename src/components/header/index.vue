<!--
  创建人：AhnSohee
  创建时间： 2020-02-02
  页面描述: 网站一级头部菜单
-->
<template>
  <!--头部菜单-->
  <header class="dn-main-header">
    <div class="wrap-outer">
      <div class="header-wrap">
        <!--logo-->
        <div
          class="logo-img"
          v-if="logoSrc"
          @click="logoClick">
          <img class="img" :src="logoSrc" alt=""/>
        </div>
        <!--菜单-->
        <dn-menu
          :default-active="defaultActive"
          class="menu"
          mode="horizontal"
          :list="list"
          @select="select">
        </dn-menu>
        <!--右侧按钮-->
        <ul class="btn-list" v-if="btnList">
          <li class="item" v-for="e in btnList" :key="e.value" @click="btnClick(e)">
            {{e.label}}
          </li>
        </ul>
      </div>
    </div>
  </header>
</template>

<script>
// vuex等插件

// 组件
import DnMenu from './dn-menu'
// 枚举

// 方法

// 接口

// 常量

export default {
  name: 'DnMainHeader',

  // 组件
  components: {DnMenu},

  // 数据对象，本页面用到的所有数据
  data() {
    return {}
  },

  props: {
    // 默认选中的菜单
    defaultActive: String,
    // 菜单数据
    list: Array,
    // logo路径
    logoSrc: String,
    // 右侧按钮数据
    btnList: Array
  },

  // 计算属性
  computed: {},

  // 监控
  watch: {},

  // 方法与事件处理
  methods: {
    // 点击菜单事件
    select(e) {
      this.$emit('select', e)
    },
    // 点击logo
    logoClick() {
      this.$emit('logoClick')
    },
    // 点击右侧按钮
    btnClick(e) {
      this.$emit('btnClick', e)
    }
  },

  // 组件生命周期钩子，一般常用的是 mounted
  mounted() {
  }
}
</script>

<style lang="stylus">
  @import "../../styles/vars.styl"
  .dn-main-header
    background $c-primary-normal

    .header-wrap
      width $w-primary
      margin auto


      .logo-img
        display inline-block
        float left
        margin 10px 50px 0 5px
        cursor pointer
        outline none

        .img
          height 30px
          width auto

      .menu
        display inline-block
        vertical-align bottom

      .el-menu
        border-bottom none
        background-color transparent!important

        .el-menu-item
          font-size 16px
          height 50px
          line-height 50px
          color #FFFFFF
          border-bottom none
          padding 0 15px

          &.is-active
            background $c-primary-hover
            color #FFFFFF

          &:hover
            background $c-primary-hover
            color #FFFFFF
            border-bottom none

        .logo-img
          display inline-block
          float left
          margin 10px 50px 0 5px
          cursor pointer
          outline none

          .img
            height 30px
            width auto

      .el-submenu
        &.is-active
          background $c-primary-hover !important
          color #FFFFFF

          .el-submenu__title
            border-bottom none

        .el-submenu__title
          font-size 16px
          height 50px
          line-height 50px
          color #fff !important
          border-bottom none
          padding 0 15px

          &.is-active
            background $c-primary-hover !important
            color #FFFFFF

          &:hover
            background $c-primary-hover
            color #FFFFFF
            border-bottom none

          .el-submenu__icon-arrow
            color white

      .el-menu--popup
        min-width 140px !important

      .more-submenu-box
        .el-menu--popup
          .el-menu-item
            min-width 140px !important

      .btn-list
        float right
        height 50px

        &:focus
          outline: 0

        .item
          cursor pointer
          padding 0 5px
          color #FFFFFF
          font-size 12px
          height 50px
          line-height 50px
          display inline-block

          i
            font-size 20px

    @media screen and (min-width: 768px)
      .wrap-outer
        margin-left calc(100vw - 100%)

</style>
