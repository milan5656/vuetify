<template>
  <v-layout>
    <div>
      Edit this <span v-html="contributionPageGithub" /> | <span v-html="contributionLanguageGithub" /> on Github
    </div>
    <v-spacer />
    <span v-html="contributionGuide" />
  </v-layout>
</template>

<script>
  // Utilities
  import {
    mapGetters,
    mapState
  } from 'vuex'
  import { parseLink } from '@/util/helpers'

  export default {
    computed: {
      ...mapGetters('documentation', [
        'namespace',
        'page'
      ]),
      ...mapState('route', ['params']),
      contributionGuide () {
        return this.parseLink('', 'Contribution Guide', `/${this.params.lang}/getting-started/contributing`)
      },
      contributionLanguageGithub () {
        return this.parseLink('', 'language', this.contributionLanguageLink)
      },
      contributionPageGithub () {
        return this.parseLink('', 'page', this.contributionPageLink)
      },
      contributionLanguageLink () {
        const file = `${this.params.namespace}/${this.page}.json`
        return `https://github.com/vuetifyjs/vuetify/tree/master/packages/vuetifyjs.com/src/lang/${this.lang}/${file}`
      },
      contributionPageLink () {
        const file = `${this.params.namespace}/${this.page}.json`
        return `https://github.com/vuetifyjs/vuetify/tree/master/packages/vuetifyjs.com/src/data/pages/${file}`
      }
    },

    methods: {
      parseLink
    }
  }
</script>
