<template>
  <div class="app">
    <div>
      <header>
        <h1 class="title">TETR.IO Emote List</h1>
        <div class="links">
          <h3 class="h3">TETR.IO</h3>
          <a href="https://tetr.io/" target="_blank">
            <vs-button rel="noopener noreferrer"> Website </vs-button>
          </a>
          <a href="https://tetr.io/about" target="_blank">
            <vs-button rel="noopener noreferrer"> About </vs-button>
          </a>
          <a href="https://discord.gg/ufDb2XJ" target="_blank">
            <vs-button rel="noopener noreferrer"> Discord </vs-button>
          </a>
        </div>
      </header>
      <br />
      <div id="emj">
        <dl class="emojis">
          <h3>Base Emotes</h3>
          <div
            v-for="(emote, index) in Object.values(emotes.base)"
            :key="index"
            @click="copyEmojo"
          >
            <dt>
              <img
                :src="'https://tetr.io/res/' + emote"
                :alt="`:${Object.keys(emotes.base)[index]}:`"
              />
            </dt>
            <dd>:{{ Object.keys(emotes.base)[index] }}:</dd>
          </div>
        </dl>
        <dl class="emojis">
          <h3>Supporter Emotes (need Patreon tier Quad or above)</h3>
          <div
            v-for="(emote, index) in Object.values(emotes.supporter)"
            :key="index"
            @click="copyEmojo"
          >
            <dt>
              <img
                :src="'https://tetr.io/res/' + emote"
                :alt="`:${Object.keys(emotes.supporter)[index]}:`"
              />
            </dt>
            <dd>:{{ Object.keys(emotes.supporter)[index] }}:</dd>
          </div>
        </dl>
        <dl class="emojis">
          <h3>Staff Emotes</h3>
          <div
            v-for="(emote, index) in Object.values(emotes.staff)"
            :key="index"
            @click="copyEmojo"
          >
            <dt>
              <img
                :src="'https://tetr.io/res/' + emote"
                :alt="`:${Object.keys(emotes.staff)[index]}:`"
              />
            </dt>
            <dd>:{{ Object.keys(emotes.staff)[index] }}:</dd>
          </div>
        </dl>
      </div>

      <!-- <h3>Supporter Emotes (need Patreon tier Quad or above)</h3>
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
      </vs-row> -->
      <br />
      <footer>
        <h4>Made haphazardly by Jabster28#6048</h4>
      </footer>
    </div>
  </div>
</template>

<script lang="ts">
/* eslint-disable no-eval */
import Vue from 'vue'
import axios from 'axios'

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
  methods: {
    copyEmojo(self: { target: HTMLElement }) {
      const selection = window.getSelection()
      const range = document.createRange()
      const dd = self.target

      if (dd.classList.contains('success')) {
        return
      }

      range.selectNodeContents(dd.childNodes[0])
      selection?.removeAllRanges()
      selection?.addRange(range)

      document.execCommand('copy')
      selection?.removeAllRanges()

      const original = dd.textContent
      dd.textContent = 'copied!'
      dd.classList.add('success')

      setTimeout(() => {
        dd.textContent = original
        dd.classList.remove('success')
      }, 1200)
    },
  },
})
</script>

<style>
#emj {
  display: flex;
  align-items: baseline;
}
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

dl.emojis {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(15em, max-content));
  grid-row-gap: 5px;
}

dl.emojis div {
  cursor: pointer;
}

dl.emojis div * {
  display: inline-block;
}

dl.emojis dt img {
  height: 20px;
  width: 20px;
  object-fit: contain;
  vertical-align: middle;
  padding-bottom: 2px;
}

dl.emojis dd {
  margin-left: 0;
  padding: 0px 8px;
}

dl.emojis dd.success {
  color: rgb(202, 143, 4);
}
</style>
