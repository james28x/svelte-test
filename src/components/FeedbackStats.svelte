<script>
  import { FeedbackStore } from "../stores";

  const { reviews } = FeedbackStore;
  $: count = $reviews.length;
  $: average =
    $reviews.reduce((sum, { rating }) => sum + rating, 0) / $reviews.length;
</script>

<div class="feedback-stats">
  <h4>{count} Reviews</h4>
  <h4>Ratings Average: {average}</h4>
</div>

<style>
  .feedback-stats {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
</style>
