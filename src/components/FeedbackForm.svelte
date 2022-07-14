<script>
  import { v4 as uuidv4 } from "uuid";
  import Card from "./Card.svelte";
  import Button from "./Button.svelte";
  import RatingSelect from "./RatingSelect.svelte";
  import { FeedbackStore } from "../stores";

  let text = "";
  let rating = 10;
  let message;
  const minText = 10;
  let btnDisabled = true;

  const handleSelect = (e) => (rating = e.detail);

  const handleSubmit = (e) => {
    if (text.trim().length >= minText) {
      const newReview = {
        id: uuidv4(),
        rating: parseInt(rating),
        text,
      };
      FeedbackStore.reviews.update((currentReviews) => {
        return [newReview, ...currentReviews];
      });
      text = "";
    }
  };

  const handleInput = () => {
    if (text.trim().length < minText) {
      btnDisabled = true;
      message = `Text must be at least ${minText} characters`;
    } else {
      btnDisabled = false;
      message = null;
    }
  };
</script>

<Card>
  <header>
    <h2>How would you rate our service with us?</h2>
  </header>
  <form on:submit|preventDefault={handleSubmit}>
    <RatingSelect on:rating-select={handleSelect} />
    <div class="input-group">
      <input
        on:input={handleInput}
        type="text"
        bind:value={text}
        placeholder="Tell us something that keeps you coming back"
      />
      <Button disabled={btnDisabled} type="submit">Send</Button>
    </div>
    {#if message}
      <div class="message">
        {message}
      </div>
    {/if}
  </form>
</Card>

<style>
  header {
    max-width: 400px;
    margin: auto;
  }

  header h2 {
    font-size: 22px;
    font-weight: 600;
    text-align: center;
  }

  .input-group {
    display: flex;
    flex-direction: row;
    /* justify-content: space-between;
    align-items: center; */
    border-style: solid;
    border-width: 1px;
    border-color: #ccc;
    border-radius: 8px;
    padding: 8px 10px;
    margin-top: 15px;
  }

  input {
    flex-grow: 2;
    border: none;
    font-size: 16px;
  }

  input:focus {
    outline: none;
  }

  .message {
    padding-top: 10px;
    text-align: center;
    color: rebeccapurple;
  }
</style>
