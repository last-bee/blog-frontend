<template>
  <layout>
    <!-- Page Header-->
    <header class="masthead" style="background-image: url('/img/home-bg.jpg')">
      <div class="container position-relative px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
          <div class="col-md-10 col-lg-8 col-xl-7">
            <div class="site-heading">
              <h1>刘彪的博客</h1>
              <span class="subheading">学习、分享、生活</span>
            </div>
          </div>
        </div>
      </div>
    </header>
    <!-- Main Content-->
    <div class="container px-4 px-lg-5">
      <div class="row gx-4 gx-lg-5 justify-content-center">
        <div class="col-md-10 col-lg-8 col-xl-7">
          <!-- Post preview-->
          <div v-for="edge in $page.posts.edges" :key="edge.node.id">
            <div class="post-preview">
              <g-link :to="'/post/' + edge.node.id">
                <h2 class="post-title">{{ edge.node.title }}</h2>
                <!-- <h3 class="post-subtitle">Problems look mighty small from 150 miles up</h3> -->
              </g-link>
              <p class="post-meta">
                Posted by
                <a href="#!">{{ edge.node.author }}</a>
                {{ edge.node.created_at }}
              </p>
            </div>
            <!-- tags -->
            <div class="tags">
              <div class="tag" v-for="tag in edge.node.tags" :key="tag.id">
                <g-link :to="'/tag/' + tag.id">
                  {{ tag.title }}
                </g-link>
              </div>
            </div>
            <!-- Divider-->
            <hr class="my-4" />
          </div>

          <!-- Pager-->
          <pager :info="$page.posts.pageInfo"></pager>
          <!-- <div class="d-flex justify-content-end mb-4">
            <a class="btn btn-primary text-uppercase" href="#!"
              >Older Posts →</a
            >
          </div> -->
        </div>
      </div>
    </div>
  </layout>
</template>
<page-query>
query($page: Int) {
    posts: allStrapiPost(perPage: 2, page: $page) @paginate {
        pageInfo {
            totalPages
            currentPage
        }
        edges {
            node {
                id
                title
                content
                author
                created_at
                tags {
                    id
                    title
                }
            }
        }
    }
}
</page-query>
<script>
import { Pager } from 'gridsome'
export default {
    components: {
        Pager
    },
    metaInfo: {
        title: "Hello, world!",
    },
};
</script>

<style>
.home-links a {
  margin-right: 1rem;
}
.tags {
  font-size: 12px;
  display: flex;
}
.tag {
  padding: 0 5px;
}
.tag:hover {
  color: #24d;
  cursor: pointer;
}
</style>
