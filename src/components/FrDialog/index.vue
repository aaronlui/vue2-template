<template>
  <div class="fr-dialog" :class="{ 'has-footer': hasFooter }">
    <el-dialog
      :visible="value"
      :title="title"
      :width="width"
      :fullscreen="fullscreen"
      :top="top"
      :modal="modal"
      :modal-append-to-body="modalAppendToBody"
      :append-to-body="appendToBody"
      :lock-scroll="lockScroll"
      :custom-class="customClass"
      :close-on-click-modal="closeOnClickModal"
      :close-on-press-escape="closeOnPressEscape"
      :show-close="showClose"
      :before-close="beforeClose"
      :center="center"
      :destroy-on-close="destroyOnClose"
      @open="open"
      @opened="opened"
      @close="close"
      @closed="closed"
    >
      <slot slot="title" name="title" />
      <slot />
      <slot slot="footer" name="footer" />
    </el-dialog>
  </div>
</template>

<script>
export default {
  model: {
    prop: 'value',
    event: 'update:value'
  },
  props: {
    value: {
      type: Boolean,
      default: false
    },
    title: {
      type: String,
      default: ''
    },
    width: {
      type: String,
      default: '50%'
    },
    fullscreen: {
      type: Boolean,
      default: false
    },
    top: {
      type: String,
      default: '0'
    },
    modal: {
      type: Boolean,
      default: true
    },
    modalAppendToBody: {
      type: Boolean,
      default: true
    },
    appendToBody: {
      type: Boolean,
      default: false
    },
    lockScroll: {
      type: Boolean,
      default: true
    },
    customClass: {
      type: String,
      default: ''
    },
    closeOnClickModal: {
      type: Boolean,
      default: false
    },
    closeOnPressEscape: {
      type: Boolean,
      default: true
    },
    showClose: {
      type: Boolean,
      default: true
    },
    beforeClose: {
      type: Function,
      default: done => done()
    },
    center: {
      type: Boolean,
      default: false
    },
    destroyOnClose: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    // 是否有footer
    hasFooter() {
      return !!this.$slots.footer
    }
  },
  methods: {
    open() {
      this.$emit('update:value', true)

      this.$emit('open')
    },
    opened() {
      this.$emit('opened')
    },
    close() {
      this.$emit('update:value', false)

      this.$emit('close')
    },
    closed() {
      this.$emit('closed')
    }
  }
}
</script>

<style lang="scss" scoped>
.fr-dialog {

}
</style>

<style lang="scss">
@import "~@/styles/mixin";

.fr-dialog {
  .el-dialog {
    top: 50%;
    transform: translateY(-50%);

    .el-dialog__body {
      max-height: calc(90vh - 54px);
      overflow-y: auto;

      @include scrollbar;
    }
  }

  &.has-footer {
    .el-dialog__body {
      max-height: calc(90vh - 54px - 70px);
    }
  }
}
</style>
