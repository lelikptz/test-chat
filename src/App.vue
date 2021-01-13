<template>
  <div id="app">
    <section class="content">
      <chat-header/>
      <div class="flex-row">
        <div class="sidebar">
          <chat-list/>
        </div>
        <div class="main">
          <chat/>
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
  width: 20.8%
  border-right: 1px solid #333333

.main
  width: 79.2%

.flex-row
  display: flex
</style>
