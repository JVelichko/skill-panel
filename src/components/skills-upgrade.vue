<template>
    <div class="mastery__outer">
      <div class="mastery">
        <div class="mastery__icon" >
          <svg>
            <circle cx="17" cy="17" r="16"></circle>
            <template v-if="this.masteryCurr === this.masteryMax ">
              <circle id="innerCircle" cx="17" cy="17" r="12"/>
            </template>
            <template v-else>
              <path :d="drawCircle(this.masteryCurr, this.masteryMax)"></path>
            </template>
          </svg>

        </div>
        <h4 class="mastery__title">{{this.titleGen.toUpperCase()}}</h4>
      </div>
      <ul v-for="(item,index) in upgrade" :key="'id'+index" class="mastery__list">
        <li>
          <p>{{item.title}}</p>
          <div></div>
          <span>{{item.value}}</span>
        </li>
      </ul>
    </div>
</template>
<script>
  export default {
    name: "skills-upgrade",

    components: {
    },

    props: {
      masteryCurr: Number,
      masteryMax: Number,
      title: {
        type: String,
        required: false
      },
      upgrade: Array,
    },

    methods: {
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

    },
    computed: {
      titleGen: function () {
        return this.title || `MASTERY ${this.masteryCurr}/${this.masteryMax}`
      }
    }
  }
</script>

<style scoped lang="sass">
  $color-text : #ffffff
  $color-bg: #16213d
  $color-primary: #3BAA82
  $color-secondary: #FECB66

  .mastery
    display: flex
    flex-direction: row
    align-items: center

    &__outer
      padding: 10px 0

    &__icon
      border-radius: 50%
      width: 32px
      height: 32px
      margin-right: 8px
      position: relative

      circle
        fill: transparent
        stroke: $color-text
        stroke-width: 2

      circle#innerCircle
        fill: $color-text

      path
        fill: white

      svg.pie
        width: 34px
        height: 34px


    &__title
      color: $color-text
      margin-top: 0
      margin-bottom: 0

    &__list
      display: flex
      flex-direction: column
      padding-inline-start: 0

      li
        display: flex
        flex-direction: row
        align-items: center
        padding-top: 6px
        padding-bottom: 6px
        color: $color-text

        & > p
          margin-top: 0
          margin-bottom: 0

        & > div
          flex: 1
          height: 1px
          background-color: rgba($color-text,0.3)
          margin: 0 8px
          transform: translateY(5px)

        & > span
          color: $color-primary
          font-weight: 600




</style>