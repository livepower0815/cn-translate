<template>
  <div class="content">
    <div class="input">
      <h3>繁體</h3>
      <textarea v-model="inputValue" cols="30" rows="10"></textarea>
    </div>
    <div class="center">to</div>
    <div class="output">
      <h3>简体</h3>
      <textarea id="output-dom" v-model="outputValue" cols="30" rows="10"></textarea>
    </div>
  </div>
  <button class="copy-btn" data-clipboard-target="#output-dom">Click Me To Copy</button>
</template>

<script setup>
import { ref, watch, onMounted } from 'vue'
import { tw2cn } from 'cjk-conv'
import ClipboardJS from 'clipboard'

const inputValue = ref('')
const outputValue = ref('')

watch(
  () => inputValue.value,
  val => {
    outputValue.value = tw2cn(val)
  }
)

onMounted(() => {
  new ClipboardJS('.copy-btn')
})
</script>

<style lang="scss">
body {
  margin: 0;
  background: #2b2c2f;
  display: flex;
  justify-content: center;
  // align-items: center;
  height: 100vh;
  width: 100%;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #abb3bb;
  flex: 1;
  max-width: 960px;
  margin-top: 10vh;
}

.content {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  .input {
    flex: 0 0 40%;
  }
  .center {
    font-size: 26px;
    font-weight: 500;
  }
  .output {
    flex: 0 0 40%;
  }
  textarea {
    width: 100%;
    height: 40vh;
    background-color: #1d1f21;
    color: #c5c8c6;
    padding: 20px;
    box-sizing: border-box;

    overflow: auto;
    outline: none;
    box-shadow: none;
    resize: none; /*remove the resize handle on the bottom right*/
  }
}

.copy-btn {
  width: 100%;
  margin: 30px 0;
  height: 60px;
  background-color: #545457;
  color: #cbd0d6;
  font-size: 30px;
}
</style>
