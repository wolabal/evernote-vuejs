<template>
  <div class="mdEditor">
    <textarea id="editor" :value="input" @input="update"></textarea>
    <div class='preview' v-html="compiledMarkdown"></div>
  </div>
</template>

<script>
import marked from 'marked'
import _ from 'lodash'

export default {
  name: 'MarkdownEditor',
  data () {
    return {
      input: '# H1 제목 작성'
    }
  },
  computed: {
    compiledMarkdown: function () {
      return marked(this.input, { sanitize: true })
    }
  },
  methods: {
    update: _.debounce(function (e) {
      this.input = e.target.value
    }, 300)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
div
  box-sizing border-box

textarea#editor
  width 50%
  resize none
  float left
  box-sizing border-box
  height 300px

.preview
  width 50%
  float right
  text-align initial
</style>
