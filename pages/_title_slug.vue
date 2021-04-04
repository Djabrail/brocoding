<template>
  <section>
    <article class="my-8">
      <div class="text-gray-600 font-bold text-sm tracking-wide">
      </div>
      <h1 class="mt-2 text-3xl font-bold">
        {{ post.title }}
      </h1>
      <div class="mt-4 markdown" v-html="post.excerpt + '\n' + post.content">
      </div>
    </article>
  </section>
</template>



<script>
export default {
  async asyncData ({ app, params }) {
    const { data } = await app.$axios.post(`${process.env.POSTS_URL}`,
    JSON.stringify({
        filter: { published: true, title_slug: params.title_slug },
        sort: {_created:-1},
        populate: 1
      }),
    {
      headers: { 'Content-Type': 'application/json' }
    })

    return { post: data.entries[0] }
  }
}


</script>