<script setup>
    import Authenticated from "@/Layouts/AuthenticatedLayout.vue";
    import { Link } from "@inertiajs/vue3"
    import { router } from "@inertiajs/vue3"
    
    const {posts} = defineProps({
        posts: Array
    })
    
    const destroy = ({id}) => {      // 分割代入です
        router.delete(route('post.delete', {id: id}), {
            onBefore: () => confirm('削除しますが、よろしいですか？')
        })
    }
    
</script>
<template>
    <Authenticated>
        <!--AuthenticatedLayout.vueの<slot name="header">にデータ（Index）を渡す-->
       <template #header>
           <h2 class="font-semibold text-xl text-gray-800 leading-tight">
               Index 
           </h2>
       </template>

        <div class="w-3/4 mx-auto mt-8 space-y-3">
            <h1 class="font-bold text-3xl text-gray-800">Blog Name</h1>
            <div class="w-1/2 mx-auto divide-gray-200 divide-y-2">
                <!--roop-->
                <div v-for="post in posts"
                    class="space-y-5">
                   <!--title-->
                    <h2 class="mt-4 font-bold text-xl text-gray-800">
                       <Link :href="route('post.show', { id: post.id })">{{ post.title }}</link>
                    </h2>
                   <button
                       class="px-3 bg-purple-300 hover:bg-purple-400 rounded-md"
                       @click="destroy(post)"
                    >削除
                    </button>
                   <!--body-->
                   <p class="p-2">{{ post.body }}</p>
                   <small>カテゴリー: {{ post.category?.name }}</small>
                </div>
                <!--roop end-->
            </div>
        </div>
    </Authenticated>
</template>