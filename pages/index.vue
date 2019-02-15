<template>
  <div>
    <h1>allTags</h1>
    <ul>
      <li v-for="tag in allTags.edges" :key="tag.node.name">{{ tag.node.name }}</li>
    </ul>
    <h1>allProjects</h1>
    <ul>
      <li v-for="pro in allProjects.edges" :key="pro.node.name">
      <h3>{{ pro.node.name }}</h3>
      ヘッダー
      <img :src="pro.node.header" width="700px" height="300px">
      ロゴ
      <img :src="pro.node.logo" width="200px" height="200px">
      ホームページ
      <a :href="pro.node.url">{{ pro.node.url }}</a>
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