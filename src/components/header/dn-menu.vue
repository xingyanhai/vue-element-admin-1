<!--
  创建人：AhnSohee
  创建时间：2020-02-02
  页面描述：NavMenu 导航菜单组件
-->
<script>
  // 菜单ref
  const MENU_REF = `dn-menu-${parseInt(Math.random() * 100000)}`

  export default {
    name: 'DnMenu',

    // 组件
    components: {},
    // 组件渲染函数
    render (h) {
      const generateMenuItem = (item, index) => {
        if (item.children) {
          // 如果当前列有children子菜单
          const elSubMenuItem = h(
            'el-submenu',
            {
              props: this.showMenuItemProps(item),
              key: `${item.value}-${index}`
            },
            [
              h(
                'template',
                {slot: 'title'},
                this.$scopedSlots[item.value] ? this.$scopedSlots[item.value](item) : item.label
              ),
              ...item.children.map((child, index2) => {
                return generateMenuItem(child, `${index}-${index2}`)
              })
            ]
          )
          return elSubMenuItem
        } else {
          const elMenuItem = h(
            'el-menu-item',
            {
              props: this.showMenuItemProps(item),
              key: `${item.value}-${index}`
            },
            this.$scopedSlots[item.value] ? this.$scopedSlots[item.value](item) : item.label
          )
          return elMenuItem
        }
      }
      const elMenuItems = this.list.map((item, index) => {
        return generateMenuItem(item, index)
      })
      const elMenu = h(
        'el-menu',
        {
          props: this.menuProps,
          on: this.menuListeners,
          ref: MENU_REF
        },
        elMenuItems
      )
      // 组件根节点
      const eRoot = h(
        'div',
        {
          'class': {
            'dn-menu': true
          }
        },
        [elMenu]
      )
      return eRoot
    },
    // 数据对象，本页面用到的所有数据
    data () {
      return {}
    },

    props: {
      list: Array
    },

    // 计算属性
    computed: {
      // el-menu属性
      menuProps () {
        return Object.assign({}, this.$attrs)
      },
      // el-menu事件
      menuListeners () {
        return Object.assign({}, this.$listeners)
      }
    },

    // 监控
    watch: {},

    // 方法与事件处理
    methods: {
      // el-menu-item 属性
      showMenuItemProps (prop) {
        let newProp = Object.assign({index: prop.value}, prop)
        // 删除无关属性
        delete newProp.children
        return newProp
      },
    },

    // 组件生命周期钩子，一般常用的是 mounted
    mounted () {
    }
  }
</script>
