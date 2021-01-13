<template>
  <div class="chat">
    <div class="chat__header">
      <div class="date">{{ date }}</div>
    </div>
    <div class="chat__body">
      <div class="message" :class="{'message__my': item.isMy}" v-for="(item, index) in chat" :key="index">
        <div v-if="!item.isMy" class="message__user">{{ item.name }}</div>
        <div class="message__text" :class="{'message__text--blue': item.isMy}">
          {{ item.text }}
          <div class="message__date" :class="{'message__date--blue': item.isMy}">{{ item.time }}</div>
        </div>
      </div>
    </div>
    <div class="chat__footer">
      <chat-textarea @addText="addText"/>
    </div>
  </div>
</template>

<script>
import ChatTextarea from './ChatTextarea'

export default {
  name: 'Chat',
  props: {
    chat: {
      type: Array,
      default() {
        return []
      }
    }
  },
  components: {
    ChatTextarea,
  },
  data()
  {
    return {
      date: '13 января',
    }
  },
  methods: {
    addText(text) {
      this.chat.push({
        isMy: true,
        name: '',
        text: text,
        time: '11:12',
      })
    }
  }
}
</script>

<style scoped lang="sass">
.chat
  height: 100%
  display: flex
  flex-direction: column
  justify-content: flex-end
  position: relative

.chat__header
  padding: 33px 0 15px
  height: 42px
  text-align: center
  position: absolute
  top: 0
  width: 100%
  background-color: #fff
  z-index: 1

  .date
    font-size: 16px
    color: #ffffff
    background-color: #333333
    display: inline-block
    padding: 9px 49px 11px
    font-weight: 900
    border-radius: 5px

.chat__body
  display: flex
  flex-direction: column
  padding-bottom: 20px
  overflow-y: scroll
  height: calc(100vh - 190px)
  justify-content: flex-end

  .scroll
    z-index: -1

.message
  max-width: 47%
  padding: 5px 27px

  &__user
    margin-left: 23px
    color: #999999
    margin-bottom: 8px

  &__my
    align-self: flex-end

  &__text
    padding: 14px 20px
    background-color: #ebebeb
    border-radius: 5px
    position: relative

    &--blue
      background-color: #cae5ff
      padding-right: 57px

  &__date
    position: absolute
    bottom: 6px
    right: 18px
    color: #999999

    &--blue
      color: #66ccff

.chat__footer
  border-top: 1px solid #333333
  height: 92px

</style>
