<script setup lang="ts">
import { ref } from 'vue'
import { invoke } from '@tauri-apps/api/core'

const greetName = ref('')
const greetMsg = ref('')

async function greet() {
  try {
    const response = await invoke('greet', { name: greetName.value })
    greetMsg.value = response as string
  } catch (error) {
    console.error('Invoke error:', error)
    greetMsg.value = 'Error calling Rust command'
  }
}
</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-purple-500 to-pink-500 flex items-center justify-center p-4">
    <div class="bg-white rounded-2xl shadow-2xl p-8 max-w-md w-full">
      <div class="text-center mb-8">
        <h1 class="text-4xl font-bold text-gray-800 mb-2">Welcome to Tauri!</h1>
        <p class="text-gray-600">A modern desktop app framework with Vue + Tailwind</p>
      </div>

      <div class="space-y-4">
        <div>
          <label for="name" class="block text-sm font-medium text-gray-700 mb-2">
            Enter your name
          </label>
          <input
            id="name"
            v-model="greetName"
            type="text"
            placeholder="Type your name..."
            class="w-full px-4 py-3 border-2 border-gray-400 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent outline-none transition-all text-gray-900 placeholder:text-gray-600"
          />
        </div>

        <button
          @click="greet()"
          class="w-full bg-purple-600 hover:bg-purple-700 text-white font-semibold py-3 px-6 rounded-lg transition-colors duration-200 shadow-md hover:shadow-lg"
        >
          Greet from Rust!
        </button>

        <p v-if="greetMsg" class="text-center text-lg font-bold p-4 bg-purple-100 rounded-lg border-2 border-purple-500 text-gray-900">
          {{ greetMsg }}
        </p>
      </div>

      <div class="mt-8 pt-6 border-t border-gray-200">
        <div class="flex items-center justify-center space-x-6 text-sm text-gray-500">
          <span class="flex items-center">
            <svg class="w-5 h-5 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
            </svg>
            Tauri v2
          </span>
          <span class="flex items-center">
            <svg class="w-5 h-5 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 21a4 4 0 01-4-4V5a2 2 0 012-2h4a2 2 0 012 2v12a4 4 0 01-4 4zm0 0h12a2 2 0 002-2v-4a2 2 0 00-2-2h-2.343M11 7.343l1.657-1.657a2 2 0 012.828 0l2.829 2.829a2 2 0 010 2.828l-8.486 8.485M7 17h.01" />
            </svg>
            Tailwind CSS
          </span>
          <span class="flex items-center">
            <svg class="w-5 h-5 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 10l-2 1m0 0l-2-1m2 1v2.5M20 7l-2 1m2-1l-2-1m2 1v2.5M14 4l-2-1-2 1M4 7l2-1M4 7l2 1M4 7v2.5M12 21l-2-1m2 1l2-1m-2 1v-2.5M6 18l-2-1v-2.5M18 18l2-1v-2.5" />
            </svg>
            Vue 3
          </span>
        </div>
      </div>
    </div>
  </div>
</template>
