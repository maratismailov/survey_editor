<script>
  import SurveyForm from "./SurveyForm.svelte";
  import ElementForm from "./ElementForm.svelte";

  export let survey;
  export let element;
  export let column;
  export let blank_column;
  export let blank_initial_field


  const add_column = () => {
    element.fields.push(column);
    column = { ...blank_column };
    document.getElementById("select_type").selectedIndex = 0;
  };
</script>

<SurveyForm {survey} {blank_initial_field}/>

<hr />

{#if survey}
  {#each survey.survey_body as element, index}
    <ElementForm {element} {index} />
    <hr />
  {/each}
{/if}
