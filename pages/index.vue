<template>
  <section class="section">
    <div class="container">
      <div class="columns is-centered is-vcentered">
        <div class="column is-8">
          <div class="box">
            <h1 class="title">
              ごちイラ イラストガチャ
            </h1>
            <h2 class="subtitle">
              なにがでるかな
            </h2>
          </div>
        </div>
      </div>
      <div class="columns is-centered is-vcentered">
        <div class="column is-8">
          <div class="box">
            <div class="columns is-centered is-vcentered">
              <div class="column is-6">
                <img class="image" src="https://placehold.jp/640x480.png">
              </div>
              <div class="column is-4">
                <div class="subtitle">
                  作品名
                </div>
                <p>
                  説明文
                </p>
              </div>
            </div>
            <div class="has-text-centered">
              <a class="button is-primary is-large">
                転載元へ
              </a>
              <br>
              <br>
              <button class="button is-medium is-secondary" @click="getArt">
                もっかいピョンピョン!
              </button>
            </div>
          </div>
        </div>
      </div>
      <div class="has-text-centered">
        <a
          class="button is-large"
          href="https://line.me"
          target="_blank"
          rel="noopener noreferrer"
        >
          <span class="icon has-text-primary">
            L
          </span>
        </a>
        <a
          class="button is-large"
          href="https://twitter.com"
          target="_blank"
          rel="noopener noreferrer"
        >
          <span class="icon has-text-info">
            T
          </span>
        </a>
      </div>
      <br>
      <div class="has-text-centered">
        <div class="columns is-centered">
          <div class="column is-2">
            <a
              href="https://gochiusa.com"
              target="_blank"
              class="has-text-centered"
            >
              Gochiusa
            </a>
          </div>
          <div class="column is-2">
            <a
              href="https://illust.gochiusa.team"
              target="_blank"
              class="has-text-centered"
            >
              Contact
            </a>
          </div>
          <div class="column is-2">
            <a
              href="https://illust.gochiusa.team"
              target="_blank"
              class="has-text-centered"
            >
              Gochiira
            </a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data () {
    return {
      illust: {}
    }
  },
  mounted () {
    this.getArt()
  },
  methods: {
    async getArt () {
      try {
        const resp = await this.$axios.get('https://api.gochiusa.team/search/random')
        this.illust = resp.data.illust
      } catch (err) {
        this.illust = {}
      }
    }
  }
}
</script>
