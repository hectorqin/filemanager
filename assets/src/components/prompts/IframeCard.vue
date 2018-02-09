<template>
  <div :class="['card', 'floating', iframeUrl === ''?'': 'iframe-card']">
    <div class="card-title" v-show="iframeUrl === ''">
      <h2>{{show}}</h2>
    </div>

    <div class="card-content">
      <p v-show="iframeUrl === ''">Please input the url of {{show}}</p>
      <input autofocus type="text" @keyup.enter="submit" v-model.trim="inputUrl">
    </div>

    <iframe class="card-iframe" v-show="iframeUrl !==''" frameborder=0 scrolling=auto :src="iframeUrl"></iframe>
  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  name: 'aria-ng',
  data: function () {
    return {
      inputUrl: '',
      iframeUrl: ''
    }
  },
  computed: {
    ...mapState(['show']),
    storageItem: function () { return this.show + '_URL' }
  },
  mounted: function () {
    console.log('mounted')
    const url = window.localStorage.getItem(this.storageItem)
    if (url) {
      this.inputUrl = url
      this.iframeUrl = url
      this.submit()
    }
  },
  methods: {
    submit: function (event) {
      let url = this.inputUrl
      if (!url.match(/^http(s)?:\/\//)) {
        url = url.substr(0, 2) === '//' ? url : ('http://' + url)
      }
      this.iframeUrl = url
      window.localStorage.setItem(this.storageItem, this.inputUrl)
    }
  }
}
</script>

