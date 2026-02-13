<template>
  <div class="page-romance relative overflow-hidden">
    <div class="floating-hearts">
      <span
        class="heart heart-1"
        aria-hidden="true"
      />
      <span
        class="heart heart-2"
        aria-hidden="true"
      />
      <span
        class="heart heart-3"
        aria-hidden="true"
      />
      <span
        class="heart heart-4"
        aria-hidden="true"
      />
      <span
        class="heart heart-5"
        aria-hidden="true"
      />
    </div>

    <UPageSection class="relative">
      <div class="mx-auto max-w-3xl text-center space-y-6">
        <p class="eyebrow">
          Valentines Day
        </p>
        <h1 class="text-5xl font-bold tracking-tight text-rose-700 sm:text-6xl">
          Will you be my Valentine, Bebi?
        </h1>
        <p class="text-lg text-rose-700/80 sm:text-xl">
          I love you with all my heart and I want to thank you for being the light of my life.
          Tap the heart to say yes. A romantic surprise will appear.
        </p>
        <p class="text-sm font-semibold uppercase tracking-[0.3em] text-rose-500">
          February 14, 2026
        </p>

        <div
          class="love-logo"
          aria-hidden="true"
        >
          <svg
            class="love-icon"
            viewBox="0 0 120 120"
          >
            <path
              d="M60 106C60 106 18 74 18 44C18 30 29 20 43 20C52 20 59 25 60 32C61 25 68 20 77 20C91 20 102 30 102 44C102 74 60 106 60 106Z"
              fill="currentColor"
            />
          </svg>
        </div>

        <div class="choice-row">
          <UButton
            label="Yes"
            color="primary"
            size="xl"
            class="choice-button choice-yes"
            @click="handleYes"
          />
          <UButton
            label="No"
            color="neutral"
            variant="outline"
            size="xl"
            class="choice-button choice-no"
          />
        </div>
      </div>
    </UPageSection>

    <Transition name="fade-slide">
      <div
        v-if="accepted"
        class="valentine-modal"
        role="dialog"
        aria-modal="true"
        aria-label="Valentines Day surprise"
        @click.self="closeModal"
      >
        <div class="valentine-backdrop" />
        <div class="valentine-card">
          <button
            type="button"
            class="modal-close"
            aria-label="Close"
            @click="closeModal"
          >
            Close
          </button>

          <div class="valentine-content">
            <UPageSection>
              <div class="romance-banner space-y-6 text-center">
                <p class="eyebrow">
                  You Said Yes
                </p>
                <h2 class="text-3xl font-semibold text-rose-700">
                  Thank you for choosing love today.
                </h2>
                <p class="text-sm text-muted">
                  This screen is filled with romance, memories, and music just for you.
                </p>
                <div class="flex flex-col items-center gap-3">
                  <CountdownTimer />
                  <UButton
                    :label="isPlaying ? 'Pause Music' : 'Play Music'"
                    color="primary"
                    variant="soft"
                    @click="toggleMusic"
                  />
                  <p class="text-xs text-muted">
                    Playing: JVKE - her (Lyrics)
                  </p>
                </div>
              </div>
            </UPageSection>

            <UPageSection id="photos">
              <div class="grid gap-8 lg:grid-cols-[0.9fr_1.1fr]">
                <div class="space-y-4">
                  <p class="eyebrow">
                    Our Story
                  </p>
                  <h3 class="text-3xl font-semibold text-rose-700">
                    A gallery of moments that feel light and bright.
                  </h3>
                  <p class="text-sm text-muted">
                    Choose two to four photos that capture the calm, joyful side of your story.
                  </p>
                </div>
                <div class="grid gap-4 sm:grid-cols-2">
                  <div
                    v-for="(photo, index) in photoGallery"
                    :key="photo"
                    class="photo-frame photo-img"
                  >
                    <img
                      :src="photo"
                      :alt="`Photo ${index + 1}`"
                      loading="lazy"
                    >
                  </div>
                </div>
              </div>
            </UPageSection>

            <UPageSection id="love-notes">
              <div class="grid gap-6 lg:grid-cols-[1.1fr_0.9fr]">
                <div class="space-y-6">
                  <p class="eyebrow">
                    Love Notes
                  </p>
                  <h3 class="text-3xl font-semibold text-rose-700">
                    Clear, heartfelt words for a beautiful love.
                  </h3>
                  <div class="grid gap-4 sm:grid-cols-2">
                    <div class="quote-card">
                      <p class="text-sm text-rose-700">
                        "Menuju WHV bersama, menjelajah dunia dan menciptakan kenangan tak terlupakan."
                      </p>
                    </div>
                    <div class="quote-card">
                      <p class="text-sm text-rose-700">
                        "Bertemu karna takdir, bersama karna cinta."
                      </p>
                    </div>
                    <div class="quote-card">
                      <p class="text-sm text-rose-700">
                        "I'm yours, no refunds."
                      </p>
                    </div>
                    <div class="quote-card">
                      <p class="text-sm text-rose-700">
                        "You are my today and all of my tomorrows."
                      </p>
                    </div>
                    <div class="quote-card">
                      <p class="text-sm text-rose-700">
                        "First date di kopi nako, alam sutra jadi saksi awal cerita kita."
                      </p>
                    </div>
                    <div class="quote-card">
                      <p class="text-sm text-rose-700">
                        "Marugame is your favorite food place, but being with you is my favorite place to be."
                      </p>
                    </div>
                  </div>
                </div>
              </div>
            </UPageSection>

            <UPageSection id="long-distance">
              <div class="romance-banner space-y-4 text-center">
                <p class="eyebrow">
                  Long Distance Love
                </p>
                <h3 class="text-3xl font-semibold text-rose-700">
                  Miles apart, hearts connected.
                </h3>
                <p class="text-sm text-muted">
                  Our love stretches from Jakarta, Indonesia to Adelaide, Australia.
                  Even across oceans and time zones, you are always in my heart.
                </p>
                <p class="text-sm font-semibold text-rose-600">
                  Maps: Jakarta, Indonesia → Adelaide, Australia
                </p>
                <p class="text-sm text-muted">
                  Total distance: ~4,556 km (great-circle)
                </p>
                <div class="mt-4 aspect-video overflow-hidden rounded-2xl border border-rose-200 bg-white">
                  <iframe
                    title="Map from Jakarta, Indonesia to Adelaide, Australia"
                    class="h-full w-full"
                    loading="lazy"
                    referrerpolicy="no-referrer-when-downgrade"
                    src="https://www.google.com/maps/embed?pb=!1m28!1m12!1m3!1d13132864.529996676!2d113.22878243645174!3d-19.7182453975048!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!4m13!3e0!4m5!1s0x2e69f3f3b7c0a3d1%3A0x6e274a5b9d8d7f83!2sJakarta%2C%20Indonesia!3m2!1d-6.2087634!2d106.845599!4m5!1s0x6ab0ce4bbf2d4b7f%3A0x3ce1fca9e1df5a0!2sAdelaide%20SA%205000%2C%20Australia!3m2!1d-34.9284989!2d138.6007456!5e0!3m2!1sen!2sid!4v1739412600000"
                  />
                </div>
              </div>
            </UPageSection>
          </div>
        </div>
      </div>
    </Transition>

    <audio
      ref="audioRef"
      loop
      preload="none"
      @play="isPlaying = true"
      @pause="isPlaying = false"
    >
      <source
        src="/audio/music.mp3"
        type="audio/mpeg"
      >
      Your browser does not support the audio element.
    </audio>
  </div>
</template>

<script setup lang="ts">
const accepted = ref(false)
const isPlaying = ref(false)
const audioRef = ref<HTMLAudioElement | null>(null)
const photoGallery = [
  '/images/IMG_0152.jpg',
  '/images/IMG_0237-2.jpg',
  '/images/img1.jpg',
  '/images/img2.jpg'
]

const handleYes = async () => {
  accepted.value = true
  await nextTick()

  if (audioRef.value) {
    try {
      await audioRef.value.play()
    } catch {
      // Autoplay may be blocked; user can press play manually.
    }
  }
}

const closeModal = () => {
  accepted.value = false
}

watch(accepted, (value) => {
  if (typeof document === 'undefined') {
    return
  }

  document.body.style.overflow = value ? 'hidden' : ''
})

onBeforeUnmount(() => {
  if (typeof document !== 'undefined') {
    document.body.style.overflow = ''
  }
})

const toggleMusic = async () => {
  if (!audioRef.value) {
    return
  }

  if (audioRef.value.paused) {
    try {
      await audioRef.value.play()
    } catch {
      // Ignore play errors.
    }
    return
  }

  audioRef.value.pause()
}
</script>
