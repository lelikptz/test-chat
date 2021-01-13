<template>
  <div class="sender">
    <div class="sender__content" ref="content" contenteditable="true"></div>
    <div class="sender__button" @click="add">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 476">
        <path
            d="M51,621V611c1.85-2.68,3.6-5.43,5.55-8,32.27-43.08,64.68-86,96.81-129.24,34.53-46.43,34.25-107.8-.36-154.14L51,183V173a23.92,23.92,0,0,1,15-14h6c1.63,1.86,4.15,1.41,6.18,2.35q42.36,19.76,84.82,39.31,99.1,45.74,198.22,91.45,93.46,43.13,187,86.19c7,3.2,12.24,7.42,14.83,14.7v9c-3.4,7.32-9.41,11.31-16.68,14.46-15.52,6.72-30.74,14.13-46.1,21.22q-79.75,36.79-159.52,73.55Q264.35,546.47,188,581.76q-58,26.71-116,53.24H66C59,632.49,53.85,628,51,621Z"
            transform="translate(-51 -159)"/>
      </svg>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Textarea',
  methods: {
    add() {
      this.$emit('addText', this.$refs.content.innerText)
      this.$refs.content.innerText = ''
    }
  }
}
</script>

<style scoped lang="sass">
.sender
  padding: 13px 20px 0 26px
  display: flex

  &__content
    padding: 2px
    font-size: 18px
    border: 1px solid
    outline: none
    height: 60px
    overflow: hidden
    overflow-y: auto
    width: 95%

  &__button
    height: 55px
    width: 55px
    fill: #000
    cursor: pointer
    transition: fill ease 300ms
    padding: 6px 0 0 10px

    &:hover
      fill: #006cff
</style>
