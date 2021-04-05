<script>
    import SelectForm from "../components/SelectForm.svelte";

    import { store_current_element } from "../stores.js";

    export let element;
    export let column;

    const unsubscribe = store_current_element.subscribe((value) => {
        element = value;
    });

    const submit_element = () => {
    console.log("blank", blank_element);
    console.log(element);
    survey.survey_body.push(element);
    survey = survey;
    element = { ...blank_element };
    element.fields = [];
    column = { ...blank_column };
  };
</script>

{#if element}
    <form on:submit|preventDefault={submit_element}>
        <div class="form_element">
            <div class="form_left">element id</div>
            <div class="form_right">
                <input bind:value={element.id} type="text" />
            </div>
        </div>

        <div class="form_element">
            <div class="form_left">element name</div>
            <div class="form_right">
                <input bind:value={element.name} type="text" />
            </div>
        </div>

        <div>
            {#if element.type == "table"}
                <div>fields:</div>
                <div>
                    <input
                        bind:value={column.id}
                        placeholder="name"
                        type="text"
                    />
                    <div id="select_type" class="select_type">
                        <label class="type_radio">
                            <input
                                type="radio"
                                bind:group={column.type}
                                value={"text"}
                            />
                            text
                        </label>
                        <label class="type_radio">
                            <input
                                type="radio"
                                bind:group={column.type}
                                value={"number"}
                            />
                            number
                        </label>
                        <label class="type_radio">
                            <input
                                type="radio"
                                bind:group={column.type}
                                value={"select"}
                            />
                            select
                        </label>
                        <button type="button" on:click={add_column}
                            >add column</button
                        >
                        <button type="submit" style="margin-left: 5px"
                            >Submit</button
                        >
                    </div>
                </div>
            {/if}
            {#if element.type == "select"}
                <SelectForm {submit_element} {element} />
            {/if}
        </div>
        {#if element.type == ""}
            <div class="select_type">
                <label class="type_radio">
                    <input
                        type="radio"
                        bind:group={element.type}
                        value={"text"}
                    />
                    text
                </label>
                <label class="type_radio">
                    <input
                        type="radio"
                        bind:group={element.type}
                        value={"number"}
                    />
                    number
                </label>
                <label class="type_radio">
                    <input
                        type="radio"
                        bind:group={element.type}
                        value={"select"}
                    />
                    select
                </label>
                <label class="type_radio">
                    <input
                        type="radio"
                        bind:group={element.type}
                        value={"table"}
                    />
                    table
                </label>
                <button type="submit">Submit</button>
            </div>
        {/if}
    </form>
{/if}

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
    .select_type {
        display: flex;
    }
    .type_radio {
        margin: 5px;
    }
</style>
