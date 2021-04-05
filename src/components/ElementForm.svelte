<script>
    import { store_current_element } from "../stores.js";

    export let element;

    const set_current_element = () => {
        store_current_element.set(element)
    };
</script>

<div on:click={set_current_element}>
    {element.id}
</div>
