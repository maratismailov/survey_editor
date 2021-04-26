<script>
    import SelectForm from "./SelectForm.svelte";

    export let element;
    export let blank_element;

    const add_column = () => {
        element.fields = [...element.fields, {...blank_element, select: {...blank_element.select}, fields: [...blank_element.fields]}];
    };
    console.log(element.fields)
</script>

<div>fields:</div>
<!-- {#if element.fields} -->
{#each element.fields as element}
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
        {#if element.type == "select"}
            <SelectForm {element} />
        {/if}
    </div>
    <div class="select_type">
        <label class="type_radio">
            <input type="radio" bind:group={element.type} value={"text"} />
            text
        </label>
        <label class="type_radio">
            <input type="radio" bind:group={element.type} value={"number"} />
            number
        </label>
        <label class="type_radio">
            <input type="radio" bind:group={element.type} value={"select"} />
            select
        </label>
        <!-- <button type="submit">Submit</button> -->
    </div>
    <hr />
    <!-- </form> -->
{/each}
<!-- {/if} -->
<button type="button" on:click={add_column}>add column</button>

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
</style>
