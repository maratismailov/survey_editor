<script>
  import { store_dictionary } from "../stores.js";

  export let survey;
  export let blank_initial_field;

  let dictionary;

  const unsubscribe = store_dictionary.subscribe((value) => {
    dictionary = value;
  });

  const add_initial_field = () => {
    survey.initial_fields = [
      ...survey.initial_fields,
      { ...blank_initial_field },
    ];
  };

  // const add_field = () => {
  //   survey.survey_body.push({...blank_element})
  //   store_survey.set(survey)
  // }
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

<button on:click={add_initial_field}>{dictionary.add_initial_field}</button>
<hr />
<div class="form_element">
  <div class="form_left">{dictionary.query_text}</div>
  <div class="form_right">
    <textarea bind:value={survey.query_text} type="text" />
  </div>
</div>
{#each survey.initial_fields as initial_field}
  <hr />
  <div class="form_element">
    <div class="form_left">{dictionary.element_id}</div>
    <div class="form_right">
      <input bind:value={initial_field.id} type="text" />
    </div>
  </div>

  <div class="form_element">
    <div class="form_left">{dictionary.element_name}</div>
    <div class="form_right">
      <input bind:value={initial_field.name} type="text" />
    </div>
  </div>
{/each}

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
  textarea { height: 200px; }
</style>
