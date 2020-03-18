<template>
  <v-card
    color="grey darken-3"
    dark
  >
    <v-card-text>
      <avatar />
      <div class="text-sm-center mb-4 mt-3">
        <h1>
          Amirreza <span class="light-blue--text text--lighten-3">Nasiri</span>
        </h1>
        <span>
          A challenge-loving web developer
        </span>
      </div>

      <sidebar-section :options="sections.info" />
      <sidebar-section :options="sections.socials" />
      <sidebar-section :options="sections.hobbies">
        <template v-slot:item="{item}">
          <v-chip>
            <v-avatar>
              <v-icon>
                {{ item.icon }}
              </v-icon>
            </v-avatar>
            {{ item.text }}
          </v-chip>
        </template>
      </sidebar-section>
      <sidebar-section :options="sections.languages">
        <template v-slot:items="{items}">
          <v-container pa-0>
            <v-layout
              wrap
              class="text-xs-center"
            >
              <template
                v-for="(item, i) in items"
              >
                <v-flex
                  :key="i"
                  md3
                  sm4
                  xs6
                >
                  <v-progress-circular
                    rotate="360"
                    size="65"
                    width="2"
                    :value="item.value"
                    color="white"
                    class="ma-2"
                  >
                    {{ item.text }}
                  </v-progress-circular>
                </v-flex>
              </template>
            </v-layout>
          </v-container>
        </template>
      </sidebar-section>
      <sidebar-section :options="{ title: 'PERSONALITY' }">
        <template>
          <v-layout>
            <v-flex xs2>
              <v-img
                src="data:image/png;base64,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"
                width="40"
              />
            </v-flex>
            <v-flex xs10>
              <div style="font-size: 1.3rem;">
                INFP - Mediator
              </div>
              <div class="grey--text">
                Read
                <a
                  href="https://www.16personalities.com/infps-at-work"
                  rel="external nofollow"
                  target="_blank"
                  class="grey--text"
                >
                  Workplace Habits
                </a>
              </div>
            </v-flex>
          </v-layout>
        </template>
      </sidebar-section>
    </v-card-text>
  </v-card>
</template>

<script>
import Avatar from '@/views/dark-template/sidebar/Avatar'
import SidebarSection from '@/views/dark-template/sidebar/Section'
export default {
  name      : 'Sidebar',
  components: { SidebarSection, Avatar },
  data () {
    return {
      sections: {
        info: {
          title: 'INFO',
          items: [
            {
              name: 'Email',
              icon: 'mdi-email',
              text: 'hi@amirreza.in',
            },
            {
              name: 'Website',
              icon: 'mdi-web',
              text: 'amirreza.in',
            },
            {
              name: 'Birth Date',
              icon: 'mdi-cake-variant',
              text: 'Dec 7, 1996',
            },
          ],
        },
        socials: {
          title: 'SOCIALS',
          items: [
            {
              icon: 'mdi-github-circle',
              text: 'github.com/AmirrezaNasiri',
              link: 'https://github.com/AmirrezaNasiri',
            },
            {
              icon: 'mdi-linkedin-box',
              text: 'linkedin.com/in/amirreza-nasiri',
              link: 'https://linkedin.com/in/amirreza-nasiri',
            },
            {
              icon: 'mdi-twitter',
              text: 'twitter.com/Amirreza_Nasiri',
              link: 'https://twitter.com/Amirreza_Nasiri',
            },
            {
              icon: 'mdi-instagram',
              text: 'instagram.com/amirreza.n96',
              link: 'https://instagram.com/amirreza.n96',
            },
          ],
        },
        hobbies: {
          title: 'HOBBIES',
          items: [

            {
              icon: 'mdi-bullseye',
              text: 'Getting out of Safe Zone',
            },
            {
              icon: 'mdi-biohazard',
              text: 'Challenges',
            },
            {
              icon: 'mdi-bike',
              text: 'Cycling',
            },
            {
              icon: 'mdi-image-filter-hdr',
              text: 'Nature',
            },
            {
              icon: 'mdi-auto-fix',
              text: 'Hacking Stuffs',
            },
            {
              icon: 'mdi-teach',
              text: 'Teaching',
            },
            {
              icon: 'mdi-karate',
              text: 'Sports',
            },
            {
              icon: 'mdi-music',
              text: 'Music',
            },
            {
              icon: 'mdi-account-group',
              text: 'Leadership',
            },
            {
              icon: 'mdi-book-open-page-variant',
              text: 'Books',
            },
            {
              icon: 'mdi-android-debug-bridge',
              text: 'Tickling Bugs!',
            },
          ],
        },
        languages: {
          title: 'LANGUAGES',
          items: [
            {
              text : 'English',
              value: 85,
            },
            {
              text : 'Turkish',
              value: 45,
            },
            {
              text : 'Azeri',
              value: 100,
            },
            {
              text : 'Persian',
              value: 100,
            },
          ],
        },
      },
    }
  },
}
</script>

<style scoped>
.sidebar{
    background: #2e2e2e;
}
</style>
