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
        <label>
          <span>Upload Avatar</span>

          <span
            class="mt-2 flex h-32 flex-col items-center justify-center gap-4 rounded-xl border border-dashed border-neutral-500 bg-neutral-700/25"
          >
            <span
              class="h-12 w-12 rounded-xl border border-neutral-700 bg-neutral-700/50 bg-[url(images/icon-upload.svg)] bg-center bg-no-repeat"
              aria-hidden="true"
            ></span>

            <span class="text-lg">Drag and drop or click to upload</span>
          </span>

          <span class="flex gap-2 pt-3 text-xs text-neutral-300"
            ><span
              class="inline-block h-4 w-4 bg-[url(images/icon-info.svg)]"
              aria-hidden="true"
            ></span
            >Upload your photo (JPG or PNG, max size: 500KB).</span
          >

          <input type="file" class="hidden" />
        </label>

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
