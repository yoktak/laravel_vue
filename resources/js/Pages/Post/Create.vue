<script setup>
  import Authenticated from '@/Layouts/AuthenticatedLayout.vue';
  import { useForm } from '@inertiajs/vue3';
  
  const {categories} = defineProps({
      categories: Array
  })
  
  const form = useForm({
      title: "",
      body: "",
      category_id: categories[0].id
  })

</script>
<template>
    <Authenticated>
        <!--AuthenticatedLayout.vueの<slot name="header">にデータ（Index）を渡す-->
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                投稿作成ページ 
            </h2>
        </template>
        <div class="mt-12 mx-auto w-1/4 p-6 bg-cyan-100 border-2 border-gray-200 flex-col rounded">
            <form @submit.prevent="form.post(route('post.store'))" >
                <!-- title-->
                <div class="m-5">
                    <label for="title">タイトル:</label>
                    <input type="text" v-model="form.title" id="title" class="w-full"/>
                    <div class="text-red-700" v-if="form.errors.title">{{ form.errors.title }}</div>
                </div>
                <!-- body -->
                <div class="m-5">
                    <label for="body">本文:</label>
                    <input type="text" v-model="form.body" id="body" class="w-full">
                    <div class="text-red-700" v-if="form.errors.body">{{ form.errors.body }}</div>
                </div>
                <!--category-->
                <div class="m-5">
                    <label for="category">カテゴリ:</label>
                    <select v-model="form.category" id="category" class="w-full">
                        <option v-for="category in categories" :value="category.id">{{ category.name}}</option>
                    </select>
                    <div class="text-red-700" v-if="form.errors.category">{{ form.errors.category }}</div>
                </div>
                <!-- submit -->
                <button
                    class="ml-auto border-2 border-gray-200 bg-cyan-100 px-2 flex"
                    type="submit"
                    :disabled="form.processing">
                    Create
                </button>
                </form>
        </div>
    </Authenticated>
</template>