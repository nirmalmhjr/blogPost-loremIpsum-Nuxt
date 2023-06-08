<template>
    <div>
        <h1>Blog Posts</h1>
        <article v-for="post in posts" :key="post.id">
            <header><strong>{{ post.id }}</strong></header>
            <p>{{ post.body }}</p>
            <NuxtLink :to="`/posts/${post.id}`">Read more &raquo;</NuxtLink>
        </article>
        <pre>{{ posts }}</pre>
    </div>
</template>

<script setup lang="ts">
    import {z} from 'zod'

    /* const postSchema = z.object({
        id: z.number(),
        title: z.string(),
        body: z.string(),
        userId:z.number(),
    })
    


    const {data: posts} = await useFetch('https://jsonplaceholder.typicode.com/posts',{
        // transform: (data)=> z.array(postSchema).parse(data)
        transform: (posts)=>{
            console.log(posts);
            return posts.map(post=> postSchema.parse(post))
        }
    }) */

    const postSchema = z.array(
        z.object({
        id: z.number(),
        title: z.string(),
        body: z.string(),
        userId:z.number(),
    })
    )

    const {data:posts} = await useFetch('https://jsonplaceholder.typicode.com/posts',{
        // transform: (data)=> z.array(postSchema).parse(data)  
        transform: (posts)=> postSchema.parse(posts)
    })

</script>

<style scoped>

</style>