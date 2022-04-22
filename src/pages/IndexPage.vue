<template>
  <q-page padding>
    <div class="q-pa-md">
      <q-table
        title="Treats"
        :rows="posts"
        :columns="columns"
        row-key="name"
      /></div
  ></q-page>
</template>

<script>
import { defineComponent, ref, onMounted } from 'vue'
import { api } from 'boot/axios'

export default defineComponent({
  name: 'IndexPage',
  setup () {
    const posts = ref([])
    const columns = [
      {
        name: 'id',
        field: 'id',
        label: 'id',
        sortable: true,
        align: 'left'
      },
      {
        name: 'title',
        field: 'title',
        label: 'Título',
        sortable: true,
        align: 'left'
      },
      {
        name: 'author',
        field: 'author',
        label: 'Autor',
        sortable: true,
        align: 'left'
      }
    ]

    onMounted(() => {
      getPosts()
    })
    const getPosts = async () => {
      try {
        const { data } = await api.get('http://localhost:3000/posts')
        posts.value = data
      } catch (error) {
        console.log(error)
      }
    }
    return {
      posts,
      columns
    }
  }
})
</script>
