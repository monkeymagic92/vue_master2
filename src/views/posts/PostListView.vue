<template>
  <div>
    <h2>게시글 목록</h2>
    <hr class="my-4" />
    <div class="row g-3">
      <div v-for="post in posts" :key="post.id" class="col-4">
        <PostItem
          :title="post.title"
          :content="post.content"
          :createdAt="post.createdAt"
          @click="goPage(post.id)"
        >
        </PostItem>
      </div>
      <hr class="my-4" />
      <AppCard>
        <PostDetailView :id="2"></PostDetailView>
      </AppCard>
    </div>
  </div>
</template>

<script setup>
import PostItem from '@/components/posts/PostItem.vue'
import PostDetailView from '@/views/posts/PostDetailView.vue'
import AppCard from '@/components/AppCard.vue'
import { getPosts } from '@/api/posts'
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const posts = ref([])
const fetchPosts = () => {
  posts.value = getPosts()
}
fetchPosts()

const goPage = (id) => {
  // 단순 url + 파라미터값을 넘기는 방법
  //   router.push('/posts/' + id)

  // name을 지정해서 객체를 넘기는 방법
  router.push({
    name: 'PostDetail',
    params: {
      id
    }
  })

  // 백틱 사용해서 문자열에 넣는방법
  // router.push(`/posts/${id}`)
}
</script>

<style lang="scss" scoped></style>
