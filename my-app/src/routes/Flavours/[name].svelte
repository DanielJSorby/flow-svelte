<script context="module">
    export async function preload({ params }) {
        const { name } = params;
        // @ts-ignore
        const flavours = JSON.parse(localStorage.getItem('flavours'));
        const flavour = flavours.find(flavour => flavour.name === name);
        return { flavour };
    }
</script>

<script>
    export let flavour;
</script>

<div>
    <h2>{flavour.name}</h2>
    <img src={flavour.image} alt={flavour.name} />
    <p>Price: {flavour.currency}{flavour.price}</p>
    <p>Main Color: {flavour.mainColor}</p>
    <p>Second Color: {flavour.secondColor}</p>
    <p>Ingredients: {flavour.ingredients.join(', ')}</p>
    <p>Caffeine: {flavour.coffeine}</p>
    <p>Vitamin: {flavour.vitamin}{flavour.vitaminType}</p>
    <p>Description: {flavour.description}</p>
</div>