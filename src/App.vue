<script setup>
	import { ref } from 'vue'

	const apiKey = ref('')
	const title = ref('')
	const markdown = ref('')
	const scheduleDate = ref(Date.now())

	const loading = ref(false)
	const error = ref(false)
	const success = ref(false)

	async function onSubmit() {
		loading.value = true

try {
		const res = await fetch('https://zealous-gray-baseball-cap.cyclic.app/schedule', {method: 'post', mode: 'cors',  headers: {'Content-Type': 'application/json'}, body: JSON.stringify({apiKey: apiKey.value, title: title.value, markdown: markdown.value, scheduleDate: scheduleDate.value})})

		success.value = true
} catch(e) {
error.value = true
}
		
		
	}
</script>

<template>
	<header class="my-16">
		<h1 class="text-2xl font-extrabold text-center">Schedule your DEV posts!</h1>
	</header>

	<main class="mx-8">
		<form 
		class="flex flex-col gap-4"
		@submit.prevent="onSubmit">
		<div class="form-field">
			<label for="api-key">DEV API Key</label>
			<input required type="text" id="api-key" v-model="apiKey"/>
		</div>

		<div class="form-field">
			<label for="title">Title</label>
			<input required type="text" id="title" v-model="title"/>

		</div>

		<div class="form-field">
			<label for="markdown">Body</label>
			<textarea  required id="markdown" v-model="markdown"></textarea>

		</div>

		<div class="form-field">

			<label for="schedule-date">Schedule date</label>
			<input type="datetime-local" id="schedule-date" v-model="scheduleDate"/>

		</div>

			<button class="bg-sky-500 rounded-lg w-full py-4 active:filter active:brightness-110 disabled:brightness-50" type="submit" :disabled="loading || error || success">{{ error ? 'Error!' : success ? 'Success!' : loading ? 'Loading...' : 'Schedule' }}</button>
		</form>

		<p v-if="error" class="mt-4 text-red-500">Something bad happened. Please reload this page.</p>
		<p class="mt-4" v-if="success">Great! Your article is now scheduled to be published on <time class="text-sky-500">{{ (new Date(scheduleDate)).toLocaleDateString() }}</time> at <time class="text-sky-500">{{ (new Date(scheduleDate)).getUTCHours() }}:00</time>!</p>
	</main>

	<footer class="fixed bottom-0 inset-x-0 pb-4 px-4">
		<p>Powered by <a class="text-sky-500 hover:underline" href="https://cyclic.sh">Cyclic</a> 💙</p>
	</footer>
</template>

<style>
.form-field {
@apply flex justify-between items-center;
}

.form-field input,
.form-field textarea {
@apply w-52 bg-slate-900;
}
</style>
