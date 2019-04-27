<template>
  <div>
    <div v-if="list.length">
      <div v-for="item in list" :key="item.id">
        <div style="padding: 0 5px;display:inline-block;width: 5px;margin-right: 15px" onselectstart="return false">
          <div class="hover" v-if="item.children && item.children.length" @click.stop="toggle(item.id)">
            <Icon v-if="extendList.includes(item.id)" type="md-arrow-dropdown" size="20"></Icon>
            <Icon v-else type="md-arrow-dropright" size="20"></Icon>
          </div>
        </div>
        <Checkbox v-model="item.checked" @on-change="setState($event, item)">{{item.title}}</Checkbox>
        <div v-if="item.children.length && extendList.includes(item.id)" style="padding-left: 20px">
          <PList :list="item.children" @setTrue="setTrue(item)"></PList>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        extendList: []
      }
    },
    name: 'PList',
    props: {
      list: {
        type: Array,
        default () {
          return []
        }
      }
    },
    watch: {
      list: {
        handler: function (val) {
          this.$emit('update:list', val)
        },
        deep: true
      }
    },
    methods: {
      toggle (id) {
        let idx = this.extendList.indexOf(id)
        if (idx >= 0) {
          this.extendList.splice(idx, 1)
        } else {
          this.extendList.push(id)
        }
      },
      setState (bool, item) {
        if (bool) {
          // 选中的时候，它的父节点、子节点都要选中，兄弟节点不管。
          this.$emit('setTrue', bool)
          if (Array.isArray(item.children) && item.children.length) this.setChildrenTrue(item.children, true)
        } else {
          // 不选中的时候，子节点都不选中，父节点、兄弟节点不管。
          if (Array.isArray(item.children) && item.children.length) this.setChildrenTrue(item.children, false)
        }
      },
      setTrue (item) {
        item.checked = true
        this.$emit('setTrue', true)
      },
      setChildrenTrue (item, bool) { // 处理 子节点 状态
        item.forEach(item => {
          item.checked = bool
          if (Array.isArray(item.children) && item.children.length) this.setChildrenTrue(item.children, bool)
        })
      }
    }
  }
</script>

<style scoped>
  .hover:hover {
    cursor: pointer;
  }
</style>
