<script>
  // import { onMount, onDestroy } from "svelte";
  import { FeedbackStore } from "../stores";
  import FeedbackItem from "./FeedbackItem.svelte";
  import { fade, scale } from "svelte/transition";

  const { reviews } = FeedbackStore;
  // let feedback = [];

  // const unsubscribe = FeedbackStore.subscribe((data) => (feedback = data));

  // onDestroy(() => {
  //   unsubscribe();
  // });
</script>

{#each $reviews as fb (fb.id)}
  <div in:scale out:fade>
    <FeedbackItem item={fb} />
  </div>
{/each}
