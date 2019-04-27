<template>
  <div class="home">
      <PList :list="testData"></PList>
  </div>
</template>

<script>
  import PList from '../components/PList'

  export default {
    name: 'home',
    components: {
      PList
    },
    data () {
      return {
        testData: [
          {
            title: 'parent 1',
            expand: true,
            checked: false,
            id: 1,
            children: [
              {
                title: 'parent 1-1',
                checked: false,
                expand: true,
                id: 11,
                children: [
                  {
                    title: 'leaf 1-1-1',
                    checked: false,
                    children: [],
                    id: 123
                  },
                  {
                    title: 'leaf 1-1-2',
                    children: [],
                    checked: false,
                    id: 201
                  }
                ]
              },
              {
                title: 'parent 1-2',
                checked: false,
                expand: true,
                id: 12,
                children: [
                  {
                    title: 'leaf 1-2-1',
                    children: [],
                    checked: false,
                    id: 100
                  },
                  {
                    title: 'leaf 1-2-1',
                    children: [],
                    checked: false,
                    id: 111
                  }
                ]
              }
            ]
          }
        ]
      }
    }
  }
</script>
