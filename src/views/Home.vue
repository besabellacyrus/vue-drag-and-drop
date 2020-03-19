<template>
  <div class="list-wrapper">
    <div
      class="item-wrapper"
      v-for="(company, index) in companies"
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
          desc: 'Create website and CMS'
        },
        {
          name: 'Sample Ph',
          position: 'Web Developer ss',
          desc: 'Web Developer sss'
        }
      ],
      draggedIndex: null,
      dragOverIndex: null
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
      }
      e.ondragover = () => {
        this.dragOverIndex = index
        // console.log({ dragover: this.dragOverIndex, dragged: this.draggedIndex })
        console.log('dragover', { dragover: this.dragOverIndex, dragged: this.draggedIndex })
        // this.array_move(this.companies, this.draggedIndex, this.dragOverIndex)
      }
      e.ondragend = () => {
        // this.array_move(this.companies, this.draggedIndex, this.dragOverIndex)
        e.setAttribute('draggable', false)
        this.array_move(this.companies, this.draggedIndex, this.dragOverIndex)
      }
    })
  },
  methods: {
    array_move (arr, draggedIndex, dragOverIndex) {
      // arr.splice(draggedIndex, 0, arr.splice(dragOverIndex, 1)[0])
      // remove the item from array
      const dragedItem = arr.splice(draggedIndex, 1)
      arr.splice(dragOverIndex, 0, ...dragedItem)
      // this.companies = arr
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
