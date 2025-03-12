<script lang="ts">
  interface Time {
    days: number;
    hours: number;
    minutes: number;
    seconds: number;
  }

  let timeLeft: Time = $state({
    days: 0,
    hours: 0,
    minutes: 0,
    seconds: 0,
  });

  function getTimeUntilNextEpisode() {
    const now = new Date();

    // Set the next episode time (Saturday 10:30 PM Pakistan time)
    const nextEpisode = new Date(now);
    nextEpisode.setUTCHours(17, 30, 0, 0); // 10:30 PM Pakistan Time = 5:30 PM UTC

    // Find the next Saturday
    nextEpisode.setUTCDate(now.getUTCDate() + ((6 - now.getUTCDay() + 7) % 7));

    // If it's already past this week's episode, move to next week
    if (now >= nextEpisode) {
      nextEpisode.setUTCDate(nextEpisode.getUTCDate() + 7);
    }

    const diffMs = nextEpisode.getTime() - now.getTime();
    const days = Math.floor(diffMs / (1000 * 60 * 60 * 24));
    const hours = Math.floor(
      (diffMs % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60),
    );
    const minutes = Math.floor((diffMs % (1000 * 60 * 60)) / (1000 * 60));
    const seconds = Math.floor((diffMs % (1000 * 60)) / 1000);

    return { days, hours, minutes, seconds };
  }

  setInterval(() => {
    timeLeft = getTimeUntilNextEpisode();
  }, 1000);
</script>

<div class="flex flex-col gap-2 justify-center items-center min-h-screen">
  <span class="text-3xl font-bold lowercase">{timeLeft?.days} days</span>
  <span class="text-3xl font-bold lowercase">{timeLeft?.hours} hours</span>
  <span class="text-3xl font-bold lowercase">{timeLeft?.minutes} minutes</span>
  <span class="text-3xl font-bold lowercase">{timeLeft?.seconds} seconds</span>
</div>
