<template>
  <div class="chat-list">
    <div class="chat-header">Чаты</div>
    <div class="chat-item" @click="selectChat(index)" v-for="(item, index) in items" :key="index">
      <div class="chat-item__title">
        <span class="text">{{ item.name }}</span><span class="time">{{ item.time }}</span>
      </div>
      <div class="chat-item__body">
        <span class="read" :class="{'active': item.isRead}">
          <svg viewBox="0 0 17 8" xmlns="http://www.w3.org/2000/svg">
            <path
                d="M16.1431 0.151334C16.2337 0.0584846 16.3567 0.00433119 16.4864 0.000226577C16.587 -0.00284044 16.6855 0.025312 16.7702 0.0796638C16.855 0.134 16.9213 0.21272 16.9606 0.305463C16.9998 0.398206 17.0101 0.500654 16.9901 0.599363C16.9702 0.698072 16.9208 0.788435 16.8486 0.858579L9.85623 7.85414C9.76251 7.94769 9.63551 8.00023 9.50311 8.00023C9.37073 8.00023 9.24373 7.94769 9.15001 7.85414L7.18408 5.88731L7.89142 5.17998L9.50661 6.79291L16.1431 0.151334Z"/>
            <path
                d="M10.4863 0.000225642C10.3566 0.00432737 10.2336 0.0584784 10.143 0.15133L3.50652 6.79291L0.859222 4.14929C0.813723 4.10202 0.759364 4.06419 0.699249 4.03794C0.639133 4.01169 0.57444 3.99754 0.508861 3.99631C0.443281 3.99508 0.378101 4.00678 0.317042 4.03074C0.255982 4.05471 0.20024 4.09048 0.152996 4.136C0.105752 4.18152 0.0679325 4.2359 0.0416967 4.29604C0.0154609 4.35619 0.00132213 4.42091 8.84642e-05 4.48652C-0.00240304 4.61902 0.0478207 4.74709 0.13971 4.84255L3.14991 7.85413C3.24364 7.94768 3.37063 8.00023 3.50303 8.00023C3.63542 8.00023 3.76241 7.94768 3.85614 7.85413L10.8485 0.85858C10.9207 0.788431 10.9701 0.698075 10.9901 0.599366C11.01 0.500657 10.9997 0.398208 10.9605 0.305461C10.9213 0.212715 10.8549 0.134004 10.7702 0.0796566C10.6854 0.0253096 10.5869 -0.00283429 10.4863 0.000225642Z"/>
          </svg>
        </span> {{ item.text }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ChatList',
  data() {
    return {
      items: [],
    }
  },
  created() {
    this.send()
  },
  methods: {
    selectChat(index) {
      this.items[index].isRead = true
      this.$emit('select', index)
    },
    send() {
      let xhr = new XMLHttpRequest()
      xhr.open('GET', 'https://orlov.tech/test.php?type=chat')
      xhr.send()
      xhr.onreadystatechange = () => {
        if (xhr.readyState === 4) {
          this.items = JSON.parse(xhr.responseText)
        }
      }
    },
  },
}
</script>

<style scoped lang="sass">
.chat-list
  padding: 15px 17px 15px 23px

.chat-header
  font-size: 18px
  font-weight: 900
  margin-bottom: 2px

.chat-item
  border-bottom: 2px solid #cccccc
  cursor: pointer
  padding-bottom: 15px
  padding-top: 15px

  &:hover
    background-color: #f3f5f5

  &__title
    display: flex
    justify-content: space-between
    margin-bottom: 10px

    .time
      color: #999999
      padding: 5px 10px 0 0

    .text
      color: #993333
      font-size: 18px
      font-weight: 900
      overflow: hidden
      white-space: nowrap
      text-overflow: ellipsis

  .read
    width: 20px
    height: 10px
    display: inline-block
    svg
      fill: #3399ff

    &.active
      svg
        fill: #000

  &__body
    overflow: hidden
    max-height: 36px

</style>
