<template>
  <div class="fr-pagination">
    <el-pagination
      :small="small"
      :background="background"
      :page-size="pageSize"
      :total="total"
      :pager-count="pagerCount"
      :current-page="currentPage"
      :layout="layout"
      :page-sizes="pageSizes"
      :popper-class="popperClass"
      :prev-text="prevText"
      :next-text="nextText"
      :disabled="disabled"
      :hide-on-single-page="hideOnSinglePage"
      @size-change="sizeChange"
      @current-change="currentChange"
      @prev-click="prevClick"
      @next-click="nextClick"
    >
      <slot />
    </el-pagination>
  </div>
</template>

<script>
export default {
  props: {
    small: {
      type: Boolean,
      default: false
    },
    background: {
      type: Boolean,
      default: true
    },
    pageSize: {
      type: Number,
      default: 10
    },
    total: {
      type: Number,
      default: 0
    },
    pagerCount: {
      type: Number,
      default: 7
    },
    currentPage: {
      type: Number,
      default: 1
    },
    layout: {
      type: String,
      default: 'total, sizes, prev, pager, next, jumper'
    },
    pageSizes: {
      type: Array,
      default() {
        return [10, 20, 30, 40, 50, 100]
      }
    },
    popperClass: {
      type: String,
      default: ''
    },
    prevText: {
      type: String,
      default: ''
    },
    nextText: {
      type: String,
      default: ''
    },
    disabled: {
      type: Boolean,
      default: false
    },
    hideOnSinglePage: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    sizeChange(size) {
      this.$emit('update:pageSize', size)
      this.$emit('update:currentPage', 1)

      this.$emit('size-change', size)
      this.$emit('change')
    },
    currentChange(page) {
      this.$emit('update:currentPage', page)

      this.$emit('current-change', page)
      this.$emit('change')
    },
    prevClick(page) {
      this.$emit('update:currentPage', page)

      this.$emit('prev-click', page)
      this.$emit('change')
    },
    nextClick(page) {
      this.$emit('update:currentPage', page)

      this.$emit('next-click', page)
      this.$emit('change')
    }
  }
}
</script>

<style lang="scss" scoped>
.fr-pagination {}
</style>

<style lang="scss">
.fr-pagination {}
</style>
