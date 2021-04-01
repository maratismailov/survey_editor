<script>
  import Parsed from "../components/Parsed.svelte";
  import Form from "../components/Form.svelte";

  let surveys = [];
  let survey = {
    survey_id: "",
    name: "",
    survey_body: [],
  };
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
  let pretty_survey = null;
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

  const show_element = () => {
    pretty_element = JSON.stringify(element, undefined, 2);
  };
  const hide_element = () => {
    pretty_element = null;
  };
  const show_survey = () => {
    pretty_survey = JSON.stringify(survey, undefined, 2);
  };

  const hide_survey = () => {
    pretty_survey = null;
  };
  const save_survey_template = async () => {
    localStorage.setItem("survey", JSON.stringify(survey));
    // const res = await fetch(
    //   `http://192.168.20.35:8000/save_survey_template?survey_id=` +
    //     survey.survey_id
    // );
    try {
      await fetch(
        `http://192.168.20.35:8000/save_survey_template?id=` +
          survey.survey_id,
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
  const delete_survey = () => {
    localStorage.setItem("survey", "");
  };
</script>

<Form {survey} {element} {column} {blank_element} {blank_column} />
<hr />

{#if !pretty_element}
  <button on:click={show_element}>show element</button>
{/if}
{#if pretty_element}
  <button on:click={hide_element}>hide element</button>
{/if}
{#if !pretty_survey}
  <button on:click={show_survey}>show survey</button>
{/if}
{#if pretty_survey}
  <button on:click={hide_survey}>hide survey</button>
{/if}
<button on:click={save_survey}>save survey</button>
<button on:click={save_survey_template}>save survey template</button>
<button on:click={delete_survey}>delete survey</button>

{#if pretty_element}
  <pre>{pretty_element}</pre>
{/if}

{#if pretty_survey}
  <pre>{pretty_survey}</pre>
{/if}

<hr />

<Parsed survey={survey.survey_body} />
