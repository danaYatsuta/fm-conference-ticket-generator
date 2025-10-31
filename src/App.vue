<script setup lang="ts">
import FormTextInput from './components/FormTextInput.vue'
import { ref, watch } from 'vue'

const state = ref<'form' | 'ticket'>('form')

const form = ref({
  name: '',
  email: '',
  github: '',
})

const formErrors = ref({
  name: '',
  email: '',
  github: '',
})

function validateName() {
  if (form.value.name === '') {
    formErrors.value.name = 'Please enter a name.'
  } else {
    formErrors.value.name = ''
  }
}

function validateEmail() {
  if (form.value.email === '') {
    formErrors.value.email = 'Please enter an email address.'
  } else if (!/^[^@]+@[^@]+$/.test(form.value.email)) {
    formErrors.value.email = 'Please enter a valid email address.'
  } else {
    formErrors.value.email = ''
  }
}

function validateGithub() {
  if (form.value.github === '') {
    formErrors.value.github = 'Please enter a GitHub username.'
  } else if (
    !/^@[a-zA-Z0-9\-]+$/.test(form.value.github) ||
    form.value.github.startsWith('@-') ||
    form.value.github.endsWith('-') ||
    form.value.github.includes('--')
  ) {
    formErrors.value.github = 'Please enter a valid GitHub username.'
  } else {
    formErrors.value.github = ''
  }
}

watch(() => form.value.name, validateName)
watch(() => form.value.email, validateEmail)
watch(
  () => form.value.github,
  () => {
    if (!form.value.github.startsWith('@')) {
      form.value.github = '@' + form.value.github
    }

    validateGithub()
  },
)

function onSubmit() {
  validateName()
  validateEmail()
  validateGithub()

  for (const formError of Object.values(formErrors.value)) {
    console.log(formError)
    if (formError !== '') return
  }

  state.value = 'ticket'
}
</script>

<template>
  <div class="background-mobile text-neutral-0 font-inconsolata min-h-dvh pt-8 text-xl">
    <header class="flex justify-center">
      <img src="./assets/images/logo-full.svg" alt="Coding Conf logo" class="w-40" />
    </header>

    <main class="px-4 pt-10">
      <template v-if="state === 'form'">
        <section class="text-center">
          <h1 class="text-3xl font-extrabold">Your Journey to Coding Conf 2025 Starts Here!</h1>

          <p class="pt-4 font-medium text-neutral-300">
            Secure your spot at next year's biggest coding conference.
          </p>
        </section>

        <form class="flex flex-col pt-8" @submit.prevent="onSubmit">
          <label class="group">
            <input type="file" class="peer h-px w-px opacity-0" />
            <span class="font-medium">Upload Avatar</span>

            <span
              class="mt-2 flex h-32 flex-col items-center justify-center gap-4 rounded-xl border border-dashed border-neutral-500 bg-neutral-700/30 outline-offset-2 outline-neutral-500 group-hover:bg-neutral-700/75 peer-focus:outline-2"
            >
              <span
                class="flex h-12 w-12 items-center justify-center rounded-xl border border-neutral-700 bg-neutral-700/50"
              >
                <img src="./assets/images/icon-upload.svg" aria-hidden="true" />
              </span>

              <span class="text-lg text-neutral-300">Drag and drop or click to upload</span>
            </span>

            <span class="flex gap-2 pt-3 text-xs text-neutral-300"
              ><img src="./assets/images/icon-info.svg" aria-hidden="true" />Upload your photo (JPG
              or PNG, max size: 500KB).</span
            >
          </label>

          <FormTextInput
            id="name"
            v-model="form.name"
            :error="formErrors.name"
            label="Full Name"
            autocomplete="name"
            class="pt-6"
          />

          <FormTextInput
            id="email"
            v-model="form.email"
            :error="formErrors.email"
            label="Email Address"
            type="email"
            placeholder="example@email.com"
            autocomplete="email"
          />

          <FormTextInput
            id="github"
            v-model="form.github"
            :error="formErrors.github"
            label="GitHub Username"
            placeholder="@yourusername"
            autocomplete="username"
          />

          <button
            type="submit"
            class="h-14 rounded-xl bg-orange-500 font-bold text-neutral-900 outline-offset-2 outline-neutral-300 hover:bg-orange-700 hover:shadow-[0_4px_var(--color-orange-500)] focus:outline-2"
          >
            Generate My Ticket
          </button>
        </form>
      </template>

      <template v-else-if="state === 'ticket'">
        <section class="text-center">
          <h1 class="text-3xl font-extrabold">
            Congrats,
            <span
              class="from-text-graident-from to-text-graident-to bg-linear-to-r bg-clip-text text-transparent"
              >{{ form.name }}</span
            >! Your ticket is ready.
          </h1>

          <p class="pt-4 font-medium text-neutral-300">
            We've emailed your ticket to
            <span class="text-text-graident-from">{{ form.email }}</span> and will send updates in
            the run up to the event.
          </p>
        </section>

        <div
          class="mt-16 flex h-40 justify-between bg-[url(images/pattern-ticket.svg)] bg-contain pt-5 pb-4 pl-4"
        >
          <div class="flex flex-col justify-between">
            <div class="flex gap-3">
              <img src="./assets/images/logo-mark.svg" alt="Coding Conf logo" class="h-8 w-8" />

              <div>
                <p class="text-2xl leading-none font-bold">Coding Conf</p>

                <p class="pt-2 text-xs text-neutral-300">Jan 31, 2025 / Austin, TX</p>
              </div>
            </div>

            <div class="flex gap-3">
              <div class="h-11 w-11 rounded-md bg-neutral-500"></div>

              <div>
                <p class="text-lg font-medium">{{ form.name }}</p>

                <p class="flex gap-1 text-xs text-neutral-300">
                  <img src="./assets/images/icon-github.svg" aria-hidden="true" class="h-4 w-4" />
                  {{ form.github }}
                </p>
              </div>
            </div>
          </div>

          <p class="rotate-90 self-center text-neutral-500">#01609</p>
        </div>
      </template>
    </main>
  </div>
</template>
