<template>
    <div>
        <article>
            <header><strong>Post ID: {{ post.id }}</strong></header>
            <h1>{{ post.title }}</h1>
            <p>{{ post.body }}</p>
            <NuxtLink to="/">Back Home</NuxtLink>
        </article>
]    </div>
</template>

<script setup lang="ts">
    import {z} from 'zod'

    const postSchema = z.object({
        id: z.number(),
        title: z.string(),
        body: z.string(),
        userId: z.number()
    })
    // const id = useRoute().params.id
    const {id} = useRoute().params

    const {data: post, error} = await useFetch(
        `https://jsonplaceholder.typicode.com/posts/${id}`,{
        transform: post=> postSchema.parse(post)
    })
    if(!post.value || error.value){
        throw createError({
            statusCode: 404,
            message: 'Post not found'
        })
    }


</script>

<style scoped>

</style>