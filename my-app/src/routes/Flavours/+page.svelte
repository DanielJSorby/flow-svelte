<script>
    import { onMount } from 'svelte';
    import Navbar from '../../Components/nabar.svelte';
    import Flavours from '../../Components/flavours.svelte';
    import Flavour from '../../Components/flavour.svelte';
    import { selectedFlavour } from '../../lib/store.js';
    import '/src/global.css';

    onMount(() => {
        selectedFlavour.set('Flavours');
    });
</script>

{#if $selectedFlavour !== 'Flavours'}
  <Navbar />
  <Flavour flavour={$selectedFlavour} />
{:else}
  <Navbar changeColor={true}/>
  <Flavours />
{/if}