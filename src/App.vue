<script setup lang="ts">
import FormTextInput from './components/FormTextInput.vue'
</script>

<template>
  <div class="background-mobile text-neutral-0 font-inconsolata h-dvh px-4 pt-8 text-xl">
    <header class="flex justify-center">
      <img src="./assets/images/logo-full.svg" alt="Coding Conf logo" class="w-40" />
    </header>

    <main class="pt-10">
      <section class="text-center">
        <h1 class="text-3xl font-extrabold">Your Journey to Coding Conf 2025 Starts Here!</h1>

        <p class="pt-4 font-medium text-neutral-300">
          Secure your spot at next year's biggest coding conference.
        </p>
      </section>

      <form class="flex flex-col gap-6 pt-8" @submit.prevent>
        <FormTextInput id="name" label="Full Name" />
        <FormTextInput
          id="email"
          label="Email Address"
          type="email"
          placeholder="example@email.com"
        />
        <FormTextInput id="github" label="GitHub Username" placeholder="@yourusername" />

        <button type="submit" class="h-14 rounded-xl bg-orange-500 font-bold text-neutral-900">
          Generate My Ticket
        </button>
      </form>
    </main>
  </div>
</template>
