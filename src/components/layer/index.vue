<template>
  <div class="modal">
    <div class="layer-bg"></div>
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header layer-head">
          <button type="button" class="close" @click="close">&times;</button>
          <h4 class="modal-title">
            {{layer.title}}
          </h4>
        </div>
        <div class="modal-body">
          <slot></slot>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-default" @click="close">关闭</button>
          <button type="button" class="btn btn-primary" v-if="layer.submitBtn" @click="submit">提交</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    props: ['layer'],
    methods: {
      close(){
        this.$emit('closelayer', false)
      },
      submit(){
          console.log("提交");
      }
    }
  }
</script>

<style lang="scss" rel="stylesheet/scss">
  /*弹层*/
  .modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }

  .layer-bg {
    top: 0;
    left: 0;
    z-index: 99;
    width: 100%;
    height: 100%;
    overflow: hidden;
  }

  .modal-dialog {
    width: 600px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate3d(-50%, -50%, 0);
  }

  .modal-content {
    background: #f5f5f5;
  }

  %layer-none {
    display: none;
  }

  %layer-bg {
    background: rgba(0, 0, 0, 0.3);
  }

  .layer-bg {
    position: fixed;
    z-index: 0;
    @extend %layer-bg;
  }

  .modal.fade.layer-detail-wrap .modal-dialog {
    transform: translate3d(100%, 0, 0);
    transition: transform .3s ease-out;
  }

  .modal.in.layer-detail-wrap .modal-dialog {
    transform: translate3d(0, 0, 0);
  }

  .layer-detail-wrap .modal-dialog {
    position: absolute;
    top: 60px;
    right: 0;
    bottom: 0;
    min-width: 800px;
    width: calc(100% - 280px);
    margin: 0;
    padding: 0;
  }

  .layer-detail {
    background: #ebebeb;
    height: 100%;
  }

  .layer-head {
    position: relative;
    padding: 10px 16px 10px 34px;
    line-height: 40px;
    background: #252834;
    font-size: 16px;
    color: #fff;
    .close {
      margin-top: 8px;
    }
  }

  .modal-footer {
    padding: 15px;
    text-align: right;
    border-top: 1px solid #e5e5e5;
  }


</style>
