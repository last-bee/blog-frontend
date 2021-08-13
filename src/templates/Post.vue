<template>
  <Layout>
    <header class="masthead" :style="{ 'backgroundImage': 'url(http://blog.lastbee.cn' + $page.post.cover.url + ')' }">
      <div class="container position-relative px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
          <div class="col-md-10 col-lg-8 col-xl-7">
            <div class="post-heading">
              <h1>{{ $page.post.title }} <span style="font-size: 16px">author: {{ $page.post.author }}</span></h1>
              <div v-html="mdToHtml($page.post.content)"></div>
            </div>
          </div>
        </div>
      </div>
    </header>
    <div>
      <g-link class="g-link" :to="'/tag/' + tag.id" v-for="tag in $page.post.tags" :key="tag.id">{{ tag.title }}</g-link>
    </div>
  </Layout>
</template>

<page-query>
query ($id: ID!){
  post: strapiPost(id: $id) {
    id
    title
    content
    author
    cover {
      url
    }
    tags {
      id
      title
    }
  }
}
</page-query>

<script>
import markdownId from 'markdown-it'
const md = new markdownId()

console.log(md)

export default {
  name: 'PostPage',
  metaInfo () {
    return {
      title: this.$page.post.title
    }
  },
  methods: {
    mdToHtml(markdown) {
      return md.render(markdown)
    }
  }
  // metaInfo: {
  //   title: ''
  // }
}
</script>

<style>
.g-link {
  padding: 0px 5px;
  font-size: 14px;
}
.g-link:hover {
  cursor: pointer;
  color: #45f;
}
</style>
