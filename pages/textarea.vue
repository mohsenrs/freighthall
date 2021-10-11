<template>
  <div class="wrapper">
    <div class="container">
      <textarea
        id="input-textarea"
        @input="inputTextArea"
        rows="12"
        ref="inputTextArea"
        placeholder="Start Typing here..."
      ></textarea>
    </div>
    <div class="count">
      <div>
        <h5 id="word-count">{{ wordCount }}</h5>
        <p>Words</p>
      </div>
      <div>
        <h5 id="charac-count">{{ characCount }}</h5>
        <p>Characters</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      characCount: 0,
      wordCount: 0,
    }
  },
  methods: {
    inputTextArea() {
      this.characCount = this.$refs.inputTextArea.value.length
      let txt = this.$refs.inputTextArea.value.trim()
      this.wordCount = txt.split(/\s+/).filter((item) => item).length
    },
  },
  // middleware({ redirect }) {
  //   if (!loggedin) {
  //     return redirect('/login')
  //   }
  // }
}
</script>

<style scoped>
.wrapper {
  position: absolute;
  width: 60vw;
  transform: translate(-50%, -50%);
  top: 50%;
  left: 50%;
}
.container {
  background-color: #ffffff;
  padding: 50px 30px 80px 30px;
  border-radius: 8px;
  box-shadow: 0 30px 50px rgba(30, 21, 49, 0.3);
}
textarea {
  width: 100%;
  border: none;
  resize: none;
  outline: none;
  font-size: 16px;
  line-height: 28px;
  color: #0e101a;
}
.count {
  background-color: #000000;
  width: 80%;
  padding: 20px;
  position: relative;
  transform: translate(-50%, -50%);
  left: 50%;
  display: flex;
  justify-content: space-around;
  text-align: center;
  border-radius: 5px;
  box-shadow: 0 20px 40px rgba(30, 21, 49, 0.4);
}
.count p {
  color: #a0a0c0;
}
.count h5 {
  color: #ffffff;
  font-size: 32px;
}
</style>
