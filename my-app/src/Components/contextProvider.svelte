<script>
    import { setContext } from 'svelte';
    import { writable } from 'svelte/store';

    const currentMainColor = writable("#454c5f"); // Set initial color
    setContext('currentMainColor', currentMainColor);
</script>

<slot />