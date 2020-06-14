<template>
  <section v-if="illust.illustID" class="section">
    <div class="container">
      <div class="columns is-centered is-vcentered">
        <div class="column is-8">
          <div class="box">
            <a class="columns is-centered is-vcentered" :href="illust.originUrl">
              <div class="column is-6 has-text-centered">
                <img :src="'https://cdn.gochiusa.team/illusts/thumb/'+illust.illustID+'.webp'">
              </div>
              <div class="column is-4">
                <div class="has-text-centered subtitle">
                  {{ illust.title }}
                </div>
              </div>
            </a>
            <div class="columns is-centered">
              <div class="column is-6">
                <div class="has-text-centered">
                  <button class="button is-medium is-primary" @click="getArt">
                    もっかいピョンピョン!
                  </button>
                </div>
              </div>
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
    </div>
  </section>
</template>

<script>
export default {
  data () {
    return {
      illust: {
        illustID: null
      }
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
        const resp = await this.$axios.get('https://api.gochiusa.team/search/random', { headers })
        this.illust = resp.data.data.imgs[0]
      } catch (err) {
        this.illust = {}
      }
    }
  }
}
</script>
