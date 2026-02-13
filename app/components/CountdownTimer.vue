<script setup lang="ts">
const timer = ref<ReturnType<typeof setInterval> | null>(null)
const targetYear = ref(new Date().getFullYear())

const timeLeft = reactive({
  days: 0,
  hours: 0,
  minutes: 0,
  seconds: 0
})

const dateFormatter = new Intl.DateTimeFormat('en-AU', {
  timeZone: 'Australia/Adelaide',
  year: 'numeric',
  month: '2-digit',
  day: '2-digit',
  hour: '2-digit',
  minute: '2-digit',
  second: '2-digit',
  hour12: false
})

const getAdelaideParts = (date: Date) => {
  const parts = dateFormatter.formatToParts(date)
  const map: Record<string, number> = {}

  for (const part of parts) {
    if (part.type !== 'literal') {
      map[part.type] = Number.parseInt(part.value, 10)
    }
  }

  return {
    year: map.year,
    month: map.month,
    day: map.day,
    hour: map.hour,
    minute: map.minute,
    second: map.second
  }
}

const toPseudoUtc = (parts: ReturnType<typeof getAdelaideParts>) => {
  return Date.UTC(
    parts.year,
    parts.month - 1,
    parts.day,
    parts.hour,
    parts.minute,
    parts.second
  )
}

const getNextValentine = (nowParts: ReturnType<typeof getAdelaideParts>, nowPseudoUtc: number) => {
  let year = nowParts.year
  let target = Date.UTC(year, 1, 14, 0, 0, 0)

  if (target <= nowPseudoUtc) {
    year += 1
    target = Date.UTC(year, 1, 14, 0, 0, 0)
  }

  targetYear.value = year
  return target
}

const updateCountdown = () => {
  const now = new Date()
  const nowParts = getAdelaideParts(now)
  const nowPseudoUtc = toPseudoUtc(nowParts)
  const targetPseudoUtc = getNextValentine(nowParts, nowPseudoUtc)
  const diff = Math.max(0, targetPseudoUtc - nowPseudoUtc)

  const totalSeconds = Math.floor(diff / 1000)
  timeLeft.days = Math.floor(totalSeconds / 86400)
  timeLeft.hours = Math.floor((totalSeconds % 86400) / 3600)
  timeLeft.minutes = Math.floor((totalSeconds % 3600) / 60)
  timeLeft.seconds = totalSeconds % 60
}

onMounted(() => {
  updateCountdown()
  timer.value = setInterval(updateCountdown, 1000)
})

onBeforeUnmount(() => {
  if (timer.value) {
    clearInterval(timer.value)
  }
})
</script>

<template>
  <div class="countdown-card">
    <p class="text-xs font-semibold uppercase tracking-[0.3em] text-rose-500">
      Adelaide Countdown
    </p>
    <p class="mt-1 text-sm text-muted">
      Next Valentine's Day: February 14, {{ targetYear }} (Australia/Adelaide)
    </p>

    <div class="mt-4 grid grid-cols-4 gap-3 text-center">
      <div class="rounded-xl bg-white/80 px-3 py-2 shadow-sm">
        <p class="text-xl font-semibold text-rose-600">
          {{ timeLeft.days }}
        </p>
        <p class="text-xs uppercase tracking-[0.2em] text-muted">
          Days
        </p>
      </div>
      <div class="rounded-xl bg-white/80 px-3 py-2 shadow-sm">
        <p class="text-xl font-semibold text-rose-600">
          {{ timeLeft.hours }}
        </p>
        <p class="text-xs uppercase tracking-[0.2em] text-muted">
          Hours
        </p>
      </div>
      <div class="rounded-xl bg-white/80 px-3 py-2 shadow-sm">
        <p class="text-xl font-semibold text-rose-600">
          {{ timeLeft.minutes }}
        </p>
        <p class="text-xs uppercase tracking-[0.2em] text-muted">
          Minutes
        </p>
      </div>
      <div class="rounded-xl bg-white/80 px-3 py-2 shadow-sm">
        <p class="text-xl font-semibold text-rose-600">
          {{ timeLeft.seconds }}
        </p>
        <p class="text-xs uppercase tracking-[0.2em] text-muted">
          Seconds
        </p>
      </div>
    </div>
  </div>
</template>
