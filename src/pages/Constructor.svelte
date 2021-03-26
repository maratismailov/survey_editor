<script>
  import Parsed from "../components/Parsed.svelte";
  import Form from '../components/Form.svelte'

  let surveys = [];
  let survey = {
    survey_id: "",
    name_ru: "",
    name_en: "",
    name_kg: "",
    survey_body: []
  };
  const blank_element = {
    id: "",
    name_ru: "",
    name_en: "",
    name_kg: "",
    type: "",
    value: "",
    fields: []
  };
  let element = { ...blank_element };

  const blank_column = {
    id: "",
    name_ru: "",
    name_en: "",
    name_kg: "",
    type: "",
    value: ""
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
  let pretty_element = "";
  let pretty_survey = "";
  let form_is_active = false;
  let table_fields = [];
  let types = ["choose type", "text", "number", "select", "table"];
  if (
    localStorage.getItem("survey") !== "" &&
    localStorage.getItem("survey") !== null
  ) {
    survey = JSON.parse(localStorage.getItem("survey"));
  } else {
    survey = survey;
  }
  if (localStorage.getItem("surveys") === null) {
    localStorage.setItem("surveys", "[]");
    surveys = JSON.parse(localStorage.getItem("surveys"));
  }
  let add_element;
  const survey_name = "nana";

  const submit_element = () => {
    console.log("blank", blank_element);
    console.log(element);
    survey.survey_body.push(element);
    survey = survey;
    // parsed_body = new Parse(survey.survey_body);
    // parsed_body = parsed_body;
    element = { ...blank_element };
    element.fields = [];
    column = { ...blank_column };
  };
  const show_element = () => {
    pretty_element = JSON.stringify(element, undefined, 2);
  };
  const show_survey = () => {
    pretty_survey = JSON.stringify(survey, undefined, 2);
  };
  const save_survey_template = () => {
    localStorage.setItem("survey", JSON.stringify(survey));
  };
  const save_survey = () => {
    surveys.push(survey);
    localStorage.setItem("surveys", JSON.stringify(surveys));
  };
  const delete_survey = () => {
    localStorage.setItem("survey", "");
  };
  const add_column = () => {
    element.fields.push(column);
    column = { ...blank_column };
    document.getElementById("select_type").selectedIndex = 0;
  };
</script>

<style>

</style>

<Parsed survey={survey.survey_body} />
<hr />

<Form survey={survey} element={element} submit_element={submit_element} column={column}/>
<hr />

<button on:click={show_element}>show element</button>
<button on:click={show_survey}>show survey</button>
<button on:click={save_survey}>save survey</button>
<button on:click={save_survey_template}>save survey template</button>
<button on:click={delete_survey}>delete survey</button>

{#if pretty_element}
  <pre>{pretty_element}</pre>
{/if}

{#if pretty_survey}
  <pre>{pretty_survey}</pre>
{/if}
