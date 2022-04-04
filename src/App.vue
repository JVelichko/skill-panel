<template>
  <div id="app">
    <skills-list :skills="skills" :active-index="0"></skills-list>
  </div>
</template>

<script>
import SkillsList from './components/skills-list.vue'

export default {
  name: 'App',
  components: {
    SkillsList
  },
  data() {
    return {
      skills: [
        {
          'name': 'Unstoppable',
          'category': 'survivability',
          'type': 'Legendary skill',
          'icon': 'stop',
          'isSelected': true,
          'desc': 'Reduce engine repair time. At last mastery level gain reduced mobility with disabled engine.',
          'masteryMax': 4,
          'masteryCurr': 1,
          'currUpgrade' : [{'title': 'Engine repair time', 'value': '-2.5%'}],
          'nextUpdradeHeading': 'upgrade on legendary rank 2',
          'nextUpgrade': [{'title': 'Engine repair time', 'value': '-5%'}],
        },
        {
          'name': 'I Come Prepared',
          'category': 'survivability',
          'type': 'skill',
          'icon': 'ready',
          'isSelected': false,
          'desc': "Improve your ship's AA armament range",
          'masteryMax': 8,
          'masteryCurr': 8,
          'currUpgrade' : [{'title': 'Firing range of AA guns', 'value': '+7.2%'}],
        },
        {
          'name': 'Punch Through',
          'category': 'confrontation',
          'type': 'skill',
          'icon': 'punch',
          'isSelected': true,
          'desc': "Increase armor-piercing capability and maximum damage of your cruiser's Ap shells",
          'masteryMax': 4,
          'masteryCurr': 3,
          'currUpgrade' : [
            {'title': "Cruiser's main gun AP shells damage", 'value':'+8%'},
            {'title': "Cruiser's AP shells penetration multiplier",'value': '+5%'} ],
          'nextUpdradeHeading': 'upgrade on legendary rank 3',
          'nextUpgrade': [
            {'title': "Cruiser's main gun AP shells damage",
              'value': '+10%'},
            {'title': "Cruiser's AP shells penetration multiplier",
              'value': '+6%'} ],
        },
      ],
    }
  },

}
</script>

<style lang="sass">
  @import url('https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@400;600;700&display=swap')
  @import "src/assets/normalize.sass"
  html, body
    overflow-x: hidden
    font-size: 18px
    font-family: 'Source Sans Pro', sans-serif

</style>
