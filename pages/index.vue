<template>
  <section v-if="illust.illustID" class="section">
    <div class="container">
      <div class="columns is-centered is-vcentered">
        <div class="column is-8">
          <div class="box">
            <a class="columns is-centered is-vcentered" :href="accessAddress">
              <div class="column is-6 has-text-centered">
                <img :src="'https://cdn.gochiusa.team/illusts/thumb/'+illust.illustID+'.jpg'">
              </div>
              <div class="column is-4">
                <div class="has-text-centered subtitle">
                  {{ illust.title }}
                </div>
              </div>
            </a>
            <div class="has-text-centered">
              <a
                class="button is-large"
                :href="'https://social-plugins.line.me/lineit/share?url=' + illust.originUrl"
                target="_blank"
                rel="noopener noreferrer"
              >
                <span class="icon has-text-primary">
                  <font-awesome-icon class="fa-lg" :icon="['fab', 'line']" />
                </span>
              </a>
              <a
                class="button is-large"
                :href="'https://twitter.com/intent/tweet?text=' + encodeURI(illust.title + '\n' + illust.originUrl)"
                target="_blank"
                rel="noopener noreferrer"
              >
                <span class="icon has-text-info">
                  <font-awesome-icon class="fa-lg" :icon="['fab', 'twitter-square']" />
                </span>
              </a>
              <a
                class="button is-large"
                href="#"
                @click="shareArt"
              >
                <span class="icon">
                  <font-awesome-icon class="fa-lg" icon="share-alt-square" />
                </span>
              </a>
            </div>
            <br>
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
    </div>
  </section>
</template>

<script>
export default {
  data () {
    return {
      illust: {
        illustID: null
      },
      isMember: this.$cookies.get('gochiira_member')
    }
  },
  computed: {
    accessAddress () {
      return this.isMember ? 'https://illust.gochiusa.team/arts/' + this.illust.illustID : this.illust.originUrl
    }
  },
  mounted () {
    this.getArt()
  },
  methods: {
    async getArt () {
      try {
        const headers = { Authorization: 'Bearer ' + 'eyJhbGciOiJIUzI1NiJ9.eyJpZCI6MSwic2VxIjozMywicGVybWlzc2lvbiI6NX0.dE9pt-BVCBVblsC7xTfxsMIrKoArmZ40saft5FFz9uY' }
        const resp = await this.$axios.get('https://api.gochiusa.team/search/random', { headers })
        this.illust = resp.data.data.imgs[0]
      } catch (err) {
        this.illust = {}
      }
    },
    async shareArt () {
      if (navigator.share) {
        const shareData = {
          title: this.illust.title,
          url: this.illust.originUrl
        }
        await navigator.share(shareData)
      } else {
        alert('サポート外のブラウザです')
      }
    }
  }
}
</script>
