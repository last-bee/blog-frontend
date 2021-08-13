<template>
  <Layout>
    <header class="masthead" style="background-image: url('/img/home-bg.jpg')">
      <div class="container position-relative px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
          <div class="col-md-10 col-lg-8 col-xl-7">
            <div class="site-heading">
              <h1>{{ $page.tag.title }}</h1>
            </div>
          </div>
        </div>
      </div>
    </header>
    <h1></h1>
    <ul>
      <li v-for="edge in $page.tag.posts" :key="edge.id">
        <g-link :to="'/post/' + edge.id ">
          {{ edge.title }}
        </g-link>
      </li>
    </ul>
  </Layout>
</template>

<page-query>
query ($id: ID!) {
  tag: strapiTag(id: $id) {
   id
   title
   posts {
     id
     title
   }
  }
}
</page-query>

<script>
</script>

