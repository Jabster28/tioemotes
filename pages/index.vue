<template>
  <div class="app">
    <div>
      <header>
        <h1 class="title">TETR.IO Emote List</h1>
        <div class="links">
          <h3 class="h3">TETR.IO</h3>
          <vs-button
            href="https://tetr.io/"
            target="_blank"
            rel="noopener noreferrer"
          >
            Website
          </vs-button>
          <vs-button
            href="https://tetr.io/about"
            target="_blank"
            rel="noopener noreferrer"
          >
            About
          </vs-button>
          <vs-button
            href="https://discord.gg/ufDb2XJ"
            target="_blank"
            rel="noopener noreferrer"
          >
            Discord
          </vs-button>
        </div>
      </header>
      <br />
      <h3>Base Emotes</h3>
      <vs-row :w="12" class="dark">
        <vs-card
          v-for="(emote, index) in Object.values(emotes.base)"
          :key="index"
          style="background: none"
          type="2"
          :w="3"
        >
          <template #title></template>
          <template #img
            ><img
              class="emote"
              width="100px"
              height="100px"
              :src="'https://tetr.io/res/' + emote"
          /></template>
          <template #text>:{{ Object.keys(emotes.base)[index] }}:</template>
        </vs-card>
      </vs-row>
      <h3>Supporter Emotes (need Patreon tier Quad or above)</h3>
      <vs-row :w="12" class="dark">
        <vs-card
          v-for="(emote, index) in Object.values(emotes.supporter)"
          :key="index"
          style="background: none"
          type="2"
          :w="3"
        >
          <template #title></template>
          <template #img
            ><img
              class="emote"
              width="100px"
              height="100px"
              :src="'https://tetr.io/res/' + emote"
          /></template>
          <template #text
            >:{{ Object.keys(emotes.supporter)[index] }}:</template
          >
        </vs-card>
      </vs-row>
      <h3>Verifed emotes (need to have a tick)</h3>
      <vs-row :w="12" class="dark">
        <vs-card
          v-for="(emote, index) in Object.values(emotes.verified)"
          :key="index"
          style="background: none"
          type="2"
          :w="3"
        >
          <template #title></template>
          <template #img
            ><img
              class="emote"
              width="100"
              height="100"
              :src="'https://tetr.io/res/' + emote"
          /></template>
          <template #text>:{{ Object.keys(emotes.verified)[index] }}:</template>
        </vs-card>
      </vs-row>
      <h3>Staff Emotes</h3>
      <vs-row :w="12" class="dark">
        <vs-card
          v-for="(emote, index) in Object.values(emotes.staff)"
          :key="index"
          style="background: none"
          type="2"
          :w="3"
        >
          <template #title></template>
          <template #img
            ><img
              class="emote"
              width="100px"
              height="100px"
              :src="'https://tetr.io/res/' + emote"
          /></template>
          <template #text>:{{ Object.keys(emotes.staff)[index] }}:</template>
        </vs-card>
      </vs-row>
      <br />
      <footer>
        <h4>Made haphazardly by Jabster28#6048</h4>
      </footer>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import axios from 'axios'
import Logo from '~/components/Logo.vue'
import VuesaxLogo from '~/components/VuesaxLogo.vue'

export default Vue.extend({
  components: {
    // Logo,
    // VuesaxLogo,
  },
  data() {
    return {
      emotes: {
        base: {},
        supporter: {},
        verified: {},
        staff: {},
      },
    }
  },
  mounted() {
    axios
      .get('https://cors-anywhere.herokuapp.com/https://tetr.io/js/tetrio.js')
      .then((res) => {
        const data = res.data
        let emotes: any
        const jsonString = (/[a-zA-Z]*=({base:{awesome:.+?}})/.exec(data) || [
          // the array is to stop typescript thinking the exec return could be undefined
          '',
          '',
        ])[1]
        emotes = {
          base: {},
          supporter: {},
          verified: {},
          staff: {},
        }
        emotes = {
          base: {},
          supporter: {},
          verified: {},
          staff: {},
        }
        eval('emotes = ' + jsonString)
        this.emotes = emotes
      })
  },
})
</script>

<style>
.dark .emote {
  background-color: #18191c;
  color: #fff;
}
.app {
  margin: 0 auto;
  background-color: #18191c;
  color: #fff;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 55px;
  letter-spacing: 1px;
  text-transform: capitalize;
  margin: 25px 0;
}

.subtitle {
  font-weight: 300;
  font-size: 1.1rem;
  word-spacing: 2px;
  padding-bottom: 15px;
  max-width: 600px;
}

.subtitle a {
  font-weight: 500;
  color: inherit;
}

.links {
  display: flex;
  align-items: center;
  justify-content: center;
}

.content-logos {
  display: flex;
  align-items: center;
  justify-content: center;
  min-width: 500px;
}

.plus {
  font-size: 2.5rem;
  margin: 15px;
}

.h3 {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-weight: 400;
  margin: 10px;
}
</style>
