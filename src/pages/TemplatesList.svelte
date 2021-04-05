<script>
    import { onMount } from "svelte";

    import { store_survey } from "../stores.js";
    import { store_current_element } from "../stores.js";

    export let url;
    let templates_list;
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
    onMount(async () => {
        const res = await fetch(url + `/get_templates_list`);
        const result = await res.json();
        templates_list = JSON.parse(result);
    });
    const get_survey_by_id = async (id) => {
        const res = await fetch(url + `/get_template_by_id?id=` + id);
        const result = await res.json();
        store_survey.set(JSON.parse(result).survey);
        store_current_element.set(blank_element);
    };
</script>

<div>
    {#if templates_list}
        {#each templates_list as template}
            <div on:click={get_survey_by_id(template.survey_id)}>
                <div>
                    {template.survey_id}
                </div>
                <div>
                    {template.survey_name}
                </div>
                <hr />
            </div>
        {/each}
    {/if}
</div>
