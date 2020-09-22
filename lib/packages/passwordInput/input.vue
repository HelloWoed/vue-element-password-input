<template>
  <div class="text-input">
    <span class="starBox">
      <span class="starItem" v-for="(item,i) in '*'.repeat(text.length)" :key="i" unselectable="on">
        {{item}}
      </span>
    </span>
    <el-input
      class="valInput"
      onpaste="return false"
      ondragenter="return false"
      type="text"
      ref="inputText"
      v-model="value"
      clearable
      :prefix-icon="prefixIcon"
      :size="inputSize"
      @keyup.native="handelKeyup"
      @clear="clearVal"
      :placeholder="placeholder"
      :maxlength="maxlength" />
  </div>
</template>
<script>
export default {
  name: 'vue-element-password-input',
  props: {
    placeholder: {
      type: String,
      default: '请输入密码',
    },
    prefixIcon:{
      type: String,
      default: 'el-icon-lock',
    },
    inputSize: { // medium / small / mini
      type: String,
      default: '',
    },
    maxlength: { // 最大长度
      type: Number,
      default: 16,
    },
  },
  data() {
    return {
      value: '',
      text: '',
    };
  },
  watch: {
    value(val) {
      if (val) {
        if (/.*[\u4e00-\u9fa5]+.*$/.test(val)) {
          this.value = val.replace(/[\u4e00-\u9fa5]/gm, '');
          return;
        }
        this.text += val.replace(/\s*/g, '');
        if (this.text) {
          this.value = ' ';
        }
      }
    },
  },
  methods: {
    setInputPaddingLeft() {
      const inputPaddingLeft = `${this.text.length * 0.5 + 1.9}rem`;
      // document.documentElement.style.setProperty('--inputPaddingLeft', inputPaddingLeft);
      this.$refs.inputText.$el.querySelector('input').style.paddingLeft = inputPaddingLeft;
      this.$emit('input', this.text);
    },
    clearVal() {
      this.text = '';
      this.setInputPaddingLeft();
    },
    handelKeyup(e) {
      // let textVal = '';
      if (e.keyCode === 8) {
        this.text = this.text.slice(0, this.text.length - 1);
      }
      if (this.text) {
        this.value = ' ';
      }
      this.setInputPaddingLeft();
    },
  },
};
</script>
<style lang="less" scoped>
  :root{
    --inputPaddingLeft: 1.9rem;
  }
  /deep/ .valInput{
    input{
      padding-left: var(--inputPaddingLeft,1.9rem);
    }
  }
  .text-input{
    display:flex;
    align-items:center;
    flex:1;
  }
  .text{
    flex: 1;
  }
  .starBox{
      padding-left: 1.9rem;
      position: absolute;
      z-index: 100;
      .starItem{
        display: inline-block;
        width: .5rem;
        -moz-user-select: none; /*火狐*/
        -webkit-user-select: none; /*webkit浏览器*/
        -ms-user-select: none; /*IE10*/
        -khtml-user-select: none; /*早期浏览器*/
        user-select: none;
      }
  }
</style>
