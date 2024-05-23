<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated :class="headerClass">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />
        <q-toolbar-title>
          <q-avatar>
            <img src="https://cryptologos.cc/logos/tether-usdt-logo.png?v=032">
          </q-avatar>
          TokoCrypto
        </q-toolbar-title>
        <q-space />
        <q-btn dense flat round icon="brightness_6" @click="toggleDarkMode" />
      </q-toolbar>
    </q-header>

    <q-drawer show-if-above v-model="leftDrawerOpen" side="left" bordered>
      <q-list>
        <q-item-label header>Navigation</q-item-label>
        <q-item clickable v-ripple @click="navigateTo('home')">
          <q-item-section avatar>
            <q-icon name="home" />
          </q-item-section>
          <q-item-section>
            Home
          </q-item-section>
        </q-item>
        <q-item clickable v-ripple @click="navigateTo('profile')">
          <q-item-section avatar>
            <q-icon name="account_circle" />
          </q-item-section>
          <q-item-section>
            Profile
          </q-item-section>
        </q-item>
        <q-item clickable v-ripple @click="navigateTo('settings')">
          <q-item-section avatar>
            <q-icon name="settings" />
          </q-item-section>
          <q-item-section>
            Settings
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <div class="q-pa-md row items-start q-gutter-md justify-center">
        <q-card
          v-for="(card, index) in cards"
          :key="index"
          class="my-card"
          flat
          bordered
        >
          <q-img :src="card.imgSrc" />
          <q-card-section>
            <div class="text-overline text-orange-9">{{ card.overline }}</div>
            <div class="text-h5 q-mt-sm q-mb-xs">{{ card.title }}</div>
            <div class="text-caption text-grey">
              {{ card.description }}
            </div>
          </q-card-section>
          <q-card-actions>
            <q-btn flat color="green" label="Buy" />
            <q-btn flat color="red" label="Sell" />
            <q-space />
            <q-btn
              color="grey"
              round
              flat
              dense
              :icon="card.expanded ? 'keyboard_arrow_up' : 'keyboard_arrow_down'"
              @click="toggleCard(card)"
            />
          </q-card-actions>
          <q-slide-transition>
            <div v-show="card.expanded">
              <q-separator />
              <q-card-section class="text-subtitle2">
                {{ card.lorem }}
              </q-card-section>
            </div>
          </q-slide-transition>
        </q-card>
      </div>
    </q-page-container>

    <q-footer :class="footerClass">
      <q-toolbar>
        <q-toolbar-title>
          TokoCrypto
        </q-toolbar-title>
        <div>
          <q-btn flat round icon="fab fa-facebook-f" @click="openLink('https://facebook.com')" />
          <q-btn flat round icon="fab fa-twitter" @click="openLink('https://twitter.com')" />
          <q-btn flat round icon="fab fa-instagram" @click="openLink('https://instagram.com')" />
        </div>
        <q-space />
        <div>
          © 2024 TokoCrypto. All rights reserved.
        </div>
      </q-toolbar>
    </q-footer>
  </q-layout>

  <div class="q-pa-md">
    <q-carousel
      animated
      v-model="slide"
      navigation
      infinite
      :autoplay="autoplay"
      arrows
      transition-prev="slide-right"
      transition-next="slide-left"
      @mouseenter="autoplay = false"
      @mouseleave="autoplay = true"
    >
      <q-carousel-slide :name="1" img-src="https://cryptologos.cc/logos/bitcoin-btc-logo.png?v=032" />
      <q-carousel-slide :name="2" img-src="https://cryptologos.cc/logos/ethereum-eth-logo.png?v=032" />
      <q-carousel-slide :name="3" img-src="https://cryptologos.cc/logos/dogecoin-doge-logo.png?v=032" />
      <q-carousel-slide :name="4" img-src="https://cryptologos.cc/logos/pepe-pepe-logo.png?v=032" />
    </q-carousel>
  </div>
</template>

<script>
import { ref } from 'vue'
import { Dark } from 'quasar'

export default {
  setup () {
    const leftDrawerOpen = ref(false)
    const slide = ref(1)
    const autoplay = ref(true)
    const cards = ref([
      {
        imgSrc: 'https://cryptologos.cc/logos/bitcoin-btc-logo.png?v=032',
        overline: 'Overline',
        title: 'Bitcoin',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
        lorem: 'Extended content for card 1',
        expanded: false
      },
      {
        imgSrc: 'https://cryptologos.cc/logos/ethereum-eth-logo.png?v=032',
        overline: 'Overline',
        title: 'Ethereum',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
        lorem: 'Extended content for card 2',
        expanded: false
      },
      {
        imgSrc: 'https://cryptologos.cc/logos/dogecoin-doge-logo.png?v=032',
        overline: 'Overline',
        title: 'Dogecoin',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
        lorem: 'Extended content for card 3',
        expanded: false
      },
      {
        imgSrc: 'https://cryptologos.cc/logos/xrp-xrp-logo.png?v=032',
        overline: 'Overline',
        title: 'XRP',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
        lorem: 'Extended content for card 4',
        expanded: false
      },
      {
        imgSrc: 'https://cryptologos.cc/logos/hedera-hbar-logo.png?v=032',
        overline: 'Overline',
        title: 'Hedera Hashgraph',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
        lorem: 'Extended content for card 5',
        expanded: false
      },
      {
        imgSrc: 'https://cryptologos.cc/logos/ondo-finance-ondo-logo.png?v=032',
        overline: 'Overline',
        title: 'Ondo Finance',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
        lorem: 'Extended content for card 6',
        expanded: false
      },
      {
        imgSrc: 'https://cryptologos.cc/logos/pepe-pepe-logo.png?v=032',
        overline: 'Overline',
        title: 'Pepe',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
        lorem: 'Extended content for card 7',
        expanded: false
      },
      {
        imgSrc: 'https://cryptologos.cc/logos/shiba-inu-shib-logo.png?v=032',
        overline: 'Overline',
        title: 'Shiba Inu',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
        lorem: 'Extended content for card 8',
        expanded: false
      },
    ])

    const toggleCard = (card) => {
      card.expanded = !card.expanded
    }

    const openLink = (url) => {
      window.open(url, '_blank')
    }

    const navigateTo = (page) => {
      console.log(`Navigating to ${page}`)
    }

    const toggleDarkMode = () => {
      Dark.set(!Dark.isActive)
    }

    return {
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      },
      cards,
      toggleCard,
      slide,
      autoplay,
      openLink,
      navigateTo,
      toggleDarkMode,
      headerClass: Dark.isActive ? 'bg-primary text-white' : 'bg-primary text-white',
      footerClass: Dark.isActive ? 'bg-primary text-white' : 'bg-primary text-white'
    }
  }
}
</script>

<style lang="sass" scoped>
.my-card
  width: 100%
  max-width: 300px
</style>
