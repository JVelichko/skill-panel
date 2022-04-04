<template>
  <div class="skills__container">
    <div class="skills__items">
      <div class="skills__item" v-for="(skill,index) in skills" :key="toKebabCase(skill.name)" >
        <img class="skills__item-img" :src="getImgUrl(skill.icon)" :alt="skill.icon" :data-index="index" @click="handleSkillSelect">
      </div>
    </div>

    <skills-list-item :content="currentSkill" ref="skillcomp">

    </skills-list-item>
  </div>
</template>

<script>
  import SkillsListItem from "./skills-list-item";

  export default {
    name: "skills-list",

    components: {
      SkillsListItem
    },

    props: {
      skills: Array,
      activeIndex: Number,
    },

    data() {
      return {
        currentSkill: Object,
      }
    },

    methods: {
      handleSkillSelect: function (event) {
        let el = event.target;
        let index = el.dataset.index;
        this.currentSkill = this.skills[index];
        console.log('this', el);
      },

      toKebabCase: function(string) {
        return string
                .replace(/([a-z])([A-Z])/g, "$1-$2")
                .replace(/[\s_]+/g, '-')
                .toLowerCase();

      },
      getImgUrl(pet) {
        let images = require.context('../assets/', false, /\.png$/);
        return images('./' + pet + ".png")
      }

    },

    created() {
      this.currentSkill = this.skills[this.activeIndex] || this.skills[0];
    },

  }
</script>

<style lang="sass">
  $color-accent: #328978

  .skills
    &__container
      display: flex
      flex-direction: row
      margin-top: 100px

    &__items
      display: flex
      flex-direction: row
      justify-content: space-around
      align-items: flex-start
      margin-right: 40px

    &__item
      margin: 0 16px
      flex: 0 1 100px
      max-width: 100px
      border-radius: 8px
      border: solid 2px transparent

      &:hover
        cursor: pointer
        border-color: $color-accent

    &__item-img
      display: block
      max-width: 100%
      height: auto
      padding: 10px
      margin-bottom: 0

</style>