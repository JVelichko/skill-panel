<template>
  <div class="skill__container">
    <div class="skill__header">
      <img class="skill__img" :src="getImgUrl(content.icon)" :alt="content.icon">
      <div>
        <h4 class="skill__name">{{content.name}}</h4>
        <h5 class="skill__label skill__label--primary">{{content.category.toUpperCase()}}</h5>
        <h5 class="skill__label skill__label--secondary-5">{{content.type.toUpperCase()}}</h5>
      </div>
    </div>
    <div class="skill__selected" v-if="content.isSelected">
      <div class="skill__selected-icon">
      </div>
      <h3 class="skill__selected-label">SELECTED</h3>
    </div>
    <div class="skill__content">
      <p>{{content.desc}}</p>
      <skills-upgrade class="skill__mastery" :upgrade="content.currUpgrade" :mastery-curr="content.masteryCurr" :mastery-max="content.masteryMax" ></skills-upgrade>
      <template v-if="this.content.masteryCurr !== this.content.masteryMax">
        <skills-upgrade class="skill__mastery--next" :title="content.nextUpdradeHeading" :upgrade="content.nextUpgrade" :mastery-curr="(content.masteryCurr + 1)" :mastery-max="content.masteryMax" ></skills-upgrade>
      </template>
    </div>

   </div>
</template>

<script>
  import SkillsUpgrade from "./skills-upgrade";
  export default {
    name: "skills-list-item",

    components: {
      SkillsUpgrade
    },

    props: {
      content: Object,
    },

    methods: {
      addLabelHandler: function (type,value) {
        this.labels.push({'type': type, 'value': value, 'id' : 'id'+this.count});
        this.count++
      },
      getImgUrl(pet) {
        let images = require.context('../assets/', false, /\.png$/);
        return images('./' + pet + ".png")
      },
      drawCircle(curr, max) {
        let degFull = 360 / max * curr;
        let deg = degFull - 90;

        let r = 12;
        let sum = 17;

        let rad = deg * Math.PI/180;

        let x;
        let y;
        if( degFull !==360) {
          x = sum  + r*Math.cos(rad);
          y = sum  + r*Math.sin(rad);
        }

        return `M${sum},${sum} L${sum},${sum - r} A${r},${r} 1 ${degFull > 180 ? '1': '0'},1 ${x},${y} z`
      },

    }
  }
</script>

<style scoped lang="sass">

  $color-text : #ffffff
  $color-bg: #16213d
  $color-primary: #3BAA82
  $color-secondary: #FECB66

  .skill
    &__container
      width: 560px
      height: 800px
      background-color: $color-bg
      padding: 20px 16px 0
      color: $color-text

    &__header
      display: flex
      flex-direction: row
      align-items: center
      margin-bottom: 16px

    &__img
      flex: 1 0 116px
      max-width: 116px
      margin-right: 16px

    &__name
      font-size: 1.15rem
      line-height: normal
      margin-bottom: 10px
      margin-top: 0
      font-weight: 600

    &__label
      font-size: 1rem
      line-height: 1.2rem
      margin-top: 0
      font-weight: 600
      margin-bottom: 0

      &:not(:last-child)
        margin-bottom: 4px

      &--primary
        color: $color-primary

      &--secondary-5
        color: $color-secondary
        opacity: 0.5

    &__selected
      padding: 8px 16px
      color: $color-secondary
      display: flex
      flex-direction: row
      align-items: center
      background-color: rgba(255,255,255,0.1)

      &-label
        font-size: 1.4rem
        line-height: normal
        margin-bottom: 0
        margin-top: 0
        font-weight: 600

      &-icon
        height: 24px
        width: 24px
        margin-right: 16px
        background-image: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA0OTAgNDkwIiB4bWw6c3BhY2U9InByZXNlcnZlIj48cGF0aCBkPSJNNDE2IDYxIDIwNiAzNzMgNjcgMjU1bC0yNCAzMCAxNzEgMTQ0TDQ0NyA4NFoiIGZpbGw9IiNmZWNiNjYiIHN0cm9rZS13aWR0aD0iNDkuNyIgc3Ryb2tlPSIjZmVjYjY2IiBzdHJva2UtbGluZWNhcD0icm91bmQiLz48L3N2Zz4=)

    &__desc
      margin-top: 10px
      margin-bottom: 10px

    &__content
      padding: 0 16px

    &__mastery
      &:not(:last-child)
        margin-bottom: 10px

      &--next
        background-color: rgba(0,0,0,0.2)
        opacity: 0.75
        margin: 0 -16px
        padding: 10px 16px

</style>