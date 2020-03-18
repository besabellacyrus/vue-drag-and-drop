<template>
  <div class="list-wrapper">
    <div
      class="item-wrapper"
      v-for="(company, index) in computedCompanies"
      :key="index"
      draggable="false"
    >
      <h1>{{ company.name }}</h1>
      <h3>{{ company.position }}</h3>
      <p>{{ company.desc }}</p>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Home',
  data () {
    return {
      companies: [
        {
          name: 'FDM',
          position: 'Full Stack Web Developer',
          desc: 'Create web based games using Vue Js and websocket'
        },
        {
          name: 'Vervespire Tech Inc',
          position: 'Web Developer',
          desc: 'API creation for the Mobile app and Responder App API and CMS creation for the LGU'
        },
        {
          name: 'Mobext Ph',
          position: 'Web Developer',
          desc: 'Web Developer'
        }
      ],
      draggedIndex: null,
      dragOverIndex: null
    }
  },
  computed: {
    computedCompanies () {
      return this.array_move(this.companies, this.draggedIndex, this.dragOverIndex)
    }
  },
  mounted () {
    const items = document.querySelectorAll('.item-wrapper')

    items.forEach((e, index) => {
      e.ondragstart = () => {
        this.draggedIndex = index
      }
      e.onmousedown = (event) => {
        e.setAttribute('draggable', true)
        console.log('mousedown')
      }
      e.ondragover = () => {
        console.log('dragover', index)
        this.dragOverIndex = index
      }
      e.ondragend = () => {
        e.setAttribute('draggable', false)
      }
    })
  },
  methods: {
    array_move (arr, oldIndex, newIndex) {
      if (newIndex >= arr.length) {
        var k = newIndex - arr.length + 1
        while (k--) {
          arr.push(undefined)
        }
      }
      arr.splice(newIndex, 0, arr.splice(oldIndex, 1)[0])
      return arr
    }
  }
}
</script>

<style lang="scss" scoped>
.list-wrapper {
  width: 450px;
  .item-wrapper {
    padding: 1rem;
    margin-bottom: 1rem;
    &:hover {
      background-color: #fff4d3;
    }
    h1 {
      font-size: 25px;
    }
  }
}
</style>
