<template>
  <div :class="['card', 'floating', iframeUrl === ''?'': 'aria-card']">
    <div class="card-title" v-show="iframeUrl === ''">
      <h2>AriaNG</h2>
    </div>

    <div class="card-content">
      <p v-show="iframeUrl === ''">Please input the url of AriaNG</p>
      <input id="aria-ng-url-input" autofocus type="text" @keyup.enter="submit" v-model.trim="inputUrl">
    </div>

    <iframe class="aria-ng-iframe" v-show="iframeUrl !==''" frameborder=0 scrolling=auto :src="iframeUrl"></iframe>
  </div>
</template>

<script>
export default {
  name: 'aria-ng',
  data: function () {
    return {
      inputUrl: '',
      iframeUrl: ''
    }
  },
  mounted: function () {
    console.log('mounted')
    const url = window.localStorage.getItem('AriaNG_URL')
    if (url) {
      this.inputUrl = url
      this.iframeUrl = url
    }
  },
  methods: {
    submit: function (event) {
      this.iframeUrl = this.inputUrl
      window.localStorage.setItem('AriaNG_URL', this.inputUrl)
    }
  }
}
</script>

