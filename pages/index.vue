<template>
  <div>
    <h2>allTags</h2>
    <ul>
      <li v-for="tag in allTags.edges" :key="tag.node.name">{{ tag.node.name }}</li>
    </ul>
    <h2>allProjects</h2>
    <ul>
      <li v-for="pro in allProjects.edges" :key="pro.node.name">
      {{ pro.node.name }}
      <br>
      <div v-html="$md.render(pro.node.content)"></div>
      <br>
      主催者: {{ pro.node.user.username }}
      <br>
      参加者
      <ul v-for="user in pro.node.users.edges" :key="user.node.username">
        <li>{{ user.node.username }}</li>
      </ul>
      <br>
      タグ
      <ul v-for="tag in pro.node.tags.edges" :key="tag.node.name">
        <li>{{ tag.node.name }}</li>
      </ul>
      </li>
    </ul>
  </div>
</template>

<script>
import allTags from '~/apollo/queries/allTags'
import allProjects from '~/apollo/queries/allProjects'

export default {
  data: () => ({
    allTags: {},
    allProjects: {}
  }),
  apollo: {
    allTags: {
      prefetch: true,
      query: allTags,
      // update: ({ user }) => user.repositories.nodes
    },
    allProjects: {
      prefetch: true,
      query: allProjects,
    }
  }
}
</script>