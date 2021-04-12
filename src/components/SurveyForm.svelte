<script>
  import { store_dictionary } from "../stores.js";

  export let survey;

  let dictionary;

  const unsubscribe = store_dictionary.subscribe((value) => {
    dictionary = value;
  });

  const show_survey = () => {
    console.log(survey);
  };
  //     const unsubscribe = survey.subscribe((value) => {
  //     survey = value;
  //   });
</script>

<div class="form_element">
  <div class="form_left">{dictionary.survey_id}</div>
  <div class="form_right">
    <input bind:value={survey.survey_id} type="text" />
  </div>
</div>

<div class="form_element">
  <div class="form_left">{dictionary.survey_name}</div>
  <div class="form_right">
    <input bind:value={survey.name} type="text" />
  </div>
</div>

<button on:click={show_survey}>show survey</button>

<style>
  .form_element {
    display: flex;
  }
  .form_left {
    width: 170px;
  }
  .form_right {
    flex-grow: 1;
  }
</style>
