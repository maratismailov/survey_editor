<script>
  import Form from "../components/Form.svelte";
  import CurrentElement from "../components/CurrentElement.svelte";

  import { store_blank_element, store_survey } from "../stores.js";
  import { store_current_element } from "../stores.js";

  let survey;
  let is_show_survey = false;
  let is_show_element = false;

  const unsubscribe = store_survey.subscribe((value) => {
    survey = value;
  });

  let surveys = [];
  // export let survey = {
  //   survey_id: "",
  //   name: "",
  //   survey_body: [],
  // };
  const blank_element = {
    id: "",
    name: "",
    type: "",
    value: "",
    fields: [],
    select: {
      table_name: "",
      name_column: "",
      where_clause: "",
      id_column: "",
    },
  };
  store_blank_element.set(blank_element);

  let element = { ...blank_element };

  const blank_column = {
    id: "",
    name_ru: "",
    name_en: "",
    name_kg: "",
    type: "",
    value: "",
  };
  let column = { ...blank_column };

  let column_types = ["choose type", "text", "number", "select"];
  let table_form = false;
  let type_is_text = false;
  let type_is_number = false;
  let type_is_select = false;
  let type_is_table = false;
  let element_type = "";

  let parsed_body = [];
  let pretty_element = null;
  let types = ["choose type", "text", "number", "select", "table"];
  // if (
  //   localStorage.getItem("survey") !== "" &&
  //   localStorage.getItem("survey") !== null
  // ) {
  //   survey = JSON.parse(localStorage.getItem("survey"));
  // } else {
  //   survey = survey;
  // }
  if (localStorage.getItem("surveys") === null) {
    localStorage.setItem("surveys", "[]");
    surveys = JSON.parse(localStorage.getItem("surveys"));
  }

  const show_element = () => {
    pretty_element = JSON.stringify(element, undefined, 2);
  };
  const hide_element = () => {
    pretty_element = null;
  };

  const save_survey_template = async () => {
    try {
      await fetch(
        `http://192.168.20.35:8000/save_survey_template?id=` + survey.survey_id,
        {
          method: "POST", // или 'PUT'
          body: JSON.stringify(survey),
          headers: {
            "Content-Type": "application/json",
          },
        }
      );
    } catch (error) {
      console.error("Ошибка:", error);
    }
  };
  const save_survey = () => {
    surveys.push(survey);
    localStorage.setItem("surveys", JSON.stringify(surveys));
  };
  // const delete_survey = () => {
  //   localStorage.setItem("survey", "");
  // };
</script>

<div>
  <div class="grid-container">
    <div>
      <Form {survey} {element} {column} {blank_element} {blank_column} />
      {#if !is_show_element}
        <button on:click={() => (is_show_element = true)}>show element</button>
      {/if}
      {#if is_show_element}
        <button on:click={() => (is_show_element = false)}>hide element</button>
      {/if}
      {#if !is_show_survey}
        <button on:click={() => (is_show_survey = true)}>show survey</button>
      {/if}
      {#if is_show_survey}
        <button on:click={() => (is_show_survey = false)}>hide survey</button>
      {/if}
      <button on:click={save_survey}>save survey</button>
      <button on:click={save_survey_template}>save survey template</button>
      <!-- <button on:click={delete_survey}>delete survey</button> -->

      {#if is_show_element}
        <pre>{JSON.stringify(element, undefined, 2)}</pre>
      {/if}
      {#if is_show_survey}
        <pre>{JSON.stringify(survey, undefined, 2)}</pre>
        <hr />
      {/if}
    </div>

    <CurrentElement {blank_element}/>
  </div>
</div>

<style>
  .grid-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr;
    gap: 15px 15px;
  }
</style>
