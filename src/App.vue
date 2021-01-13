<template>
  <div id="app">
    <section class="content">
      <chat-header/>
      <div class="flex-row">
        <div class="sidebar">
          <chat-list @select="setChat"/>
        </div>
        <div class="main">
          <chat :chat="chat"/>
        </div>
      </div>
    </section>
    <div class="mobile-app-notice">
      <div class="mobile-app-notice__text">
        Простите но для мобильных телефонов у нас есть мобильное приложение
      </div>
    </div>
  </div>
</template>

<script>
import ChatHeader from './components/ChatHeader'
import ChatList from './components/ChatList'
import Chat from './components/Chat'

export default {
  name: 'App',
  components: {
    ChatHeader,
    ChatList,
    Chat,
  },
  data(){
    return {
      chat: []
    }
  },
  methods: {
    setChat(id) {
      let xhr = new XMLHttpRequest()
      xhr.open('GET', 'https://orlov.tech/test.php?type=text&id=' + id)
      xhr.send()
      xhr.onreadystatechange = () => {
        if (xhr.readyState === 4) {
          this.chat = JSON.parse(xhr.responseText)
        }
      }
    },
  }
}
</script>

<style lang="sass">
html, body
  overflow: auto
  height: 100%
  font-size: 14px
  font-family: 'Exo 2', Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  color: #333333
  margin: 0
  padding: 0
  width: 100%

#app
  text-align: left
  width: 100%
  height: 100%
  position: relative

.mobile-app-notice
  display: none

  @media (max-width: 699px)
    display: flex
    font-size: 36px
    color: #999999
    text-align: center
    align-items: center
    justify-content: center
    height: 100%

    &__text
      margin-top: -20%
      padding: 0 10%

.chat-icon
  width: 40px
  height: 40px
  fill: #ffffff

.content
  display: flex
  height: 100%
  flex-direction: column

  @media (max-width: 699px)
    display: none

.sidebar
  width: 350px
  border-right: 1px solid #333333

.main
  width: 100%

.flex-row
  display: flex
</style>
