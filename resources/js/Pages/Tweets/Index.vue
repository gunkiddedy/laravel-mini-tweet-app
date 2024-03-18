<script setup>
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue"
import InputError from "@/Components/InputError.vue"
import PrimaryButton from "@/Components/PrimaryButton.vue"
import { useForm, Head } from "@inertiajs/vue3"
import Tweet from "@/Components/Tweet.vue"

defineProps(["tweets"])

const form = useForm({
  message: "",
})
</script>

<template>
  <Head title="Tweets" />

  <AuthenticatedLayout>
    <div class="max-w-2xl mx-auto p-4 sm:p-6 lg:p-8">
      <form
        @submit.prevent="
          form.post(route('tweets.store'), { onSuccess: () => form.reset() })
        "
      >
        <textarea
          v-model="form.message"
          placeholder="What's on your mind?"
          rows="5"
          class="block w-full border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm"
        ></textarea>
        <InputError :message="form.errors.message" class="mt-2" />
        <PrimaryButton class="mt-4">Tweet</PrimaryButton>
      </form>
      <div class="mt-6 bg-white shadow-sm rounded-lg divide-y">
        <Tweet v-for="tweet in tweets" :key="tweet.id" :tweet="tweet" />
      </div>
    </div>
  </AuthenticatedLayout>
</template>
