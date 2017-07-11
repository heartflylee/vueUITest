<template>
  <div class="modal">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="signUp-wrap">
          <div class="signUp-close" @click="signclose">
            <i>&times;</i>
          </div>
          <div class="signUp-main">
            <div class="s-title">
              {{title}}
            </div>
            <div class="s-box">
              <slot></slot>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
        title:String
    },
    methods: {
      signclose(){
          this.$emit('closeSign',false)
      }
    }
  }

</script>

<style lang="scss" rel="stylesheet/scss">


</style>
