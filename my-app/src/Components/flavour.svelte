<script>
import { onMount } from 'svelte';
    export let flavour;
    import { selectedFlavour } from '../lib/store.js'; // Import the store
    let currentFlavour;
    let amount = 1;
    function lessAmount() {
        if (amount > 1) {
            amount -= 1;
        }
    }

    function addAmount() {
        if (amount < 99) {
            amount += 1;
        }
    }

    onMount(() => {
        const storedFlavours = JSON.parse(localStorage.getItem('flavours') || 'null');
        console.log('storedFlavours:', storedFlavours); // Log storedFlavours
        console.log('flavour:', flavour); // Log flavour
        if (storedFlavours) {
            const matchingFlavour = storedFlavours.find(f => f.name === flavour);
            console.log('matchingFlavour:', matchingFlavour); // Log matchingFlavour
            if (matchingFlavour) {
                currentFlavour = matchingFlavour;
            }
        }
    });

    function goBack() {
        selectedFlavour.set('Flavours'); // Set selectedFlavour back to 'Flavours'
    }

    let addedToCart = false;
    function addToCart() {
        addedToCart = true;
        if (typeof window !== 'undefined') {
            let cart = JSON.parse(localStorage.getItem('cart') || '[]');
            const itemIndex = cart.findIndex(item => item.name === currentFlavour.name);
            if (itemIndex > -1) {
                cart[itemIndex].amount += amount;
            } else {
                cart.push({ name: currentFlavour.name, amount, image: currentFlavour.image, price: currentFlavour.price});
            }
            localStorage.setItem('cart', JSON.stringify(cart));
        }
    }
</script>

{#if currentFlavour}
    <div class="flavour-all">
        <div class="flavour-container top {currentFlavour.name}" style="background-color: {currentFlavour.mainColor}; color: {currentFlavour.secondColor}">
            <div class="flavour">
                <div class="flav-text">
                    <h1 class="flav-name">{currentFlavour.name}</h1>
                    <div class="flav-desc">
                        <p class="flav-ingredients">
                            {@html currentFlavour.ingredients ? currentFlavour.ingredients.join('<br>') : 'No ingredients listed'}
                        </p>
                        <div class="line flav-line" style="background-color: {currentFlavour.secondColor}"></div>
                        <div class="flav-nutritions">
                            <p class="flav-numbers">{currentFlavour.coffeine}<br>{currentFlavour.vitamin}</p>
                            <p class="flav-names">Coffeine<br>Vitamin {currentFlavour.vitaminType}</p>
                        </div>
                    </div>
                </div>
                <div class="flav-image">
                    <img src="{currentFlavour.image}" alt="{currentFlavour.name}" class="flav-pic">
                </div>
                <div>
                    <h1 class="flav-price">{currentFlavour.currency} {currentFlavour.price + ".00"}</h1>
                    <p>In stock</p>
                    <div class="line flav-line" style="background-color: {currentFlavour.secondColor}"></div>
                    <div class="amount-and-cart">
                        <div class="amount">
                            <button class="less" on:click={lessAmount}>-</button>
                            <p>{amount}</p>
                            <button class="add" on:click={addAmount}>+</button>
                        </div>
                        <div class="add-to-cart">
                            <button on:click={addToCart}>
                                {#if addedToCart}
                                    Added to cart
                                {:else}
                                    Add to cart &check;
                                {/if}
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="flavour-container bottom {currentFlavour.name}" style="background-color: {currentFlavour.secondColor}; color: {currentFlavour.mainColor}">
            <div class="flavour">
                <div class="flav-text">
                    <h1 class="flav-name">{currentFlavour.name}</h1>
                    <div class="flav-desc">
                        <p>{currentFlavour.description}</p>
                    </div>
                </div>
                <div class="flav-image">
                    <img src="{currentFlavour.image}" alt="{currentFlavour.name}" class="flav-pic">
                </div>
                <div>
                    <h1 class="flav-price">{currentFlavour.currency} {currentFlavour.price + ".00"}</h1>
                    <p>In stock</p>
                    <div class="line flav-line" style="background-color: {currentFlavour.secondColor}"></div>
                    <div class="amount-and-cart">
                        <div class="amount">
                            <button class="less" on:click={lessAmount}>-</button>
                            <p>{amount}</p>
                            <button class="add" on:click={addAmount}>+</button>
                        </div>
                        <div class="add-to-cart">
                            <button on:click={addToCart}>
                                {#if addedToCart}
                                    Added to cart
                                {:else}
                                    Add to cart &check;
                                {/if}
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <button class="go-back" on:click={goBack}>&lt;</button>
{:else}
    <p>No flavour selected</p>
    <button on:click={goBack}>&lt;</button>
{/if}

<style>
    .flavour-all {
        scroll-snap-type: y mandatory;
        overflow-y: scroll;
        height: 100vh;
    }
    .flavour-container {
        scroll-snap-align: start;
        width: 100%;
        height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .add-to-cart button:active {
        box-shadow: 0px 0px 0px 0px rgba(0, 0, 0, 0);
        transform: translateY(3px);
    }

    .flavour p {
        font-size: 50px;
    }

    .flavour-container.bottom .flavour .flav-desc p{
        font-size: 20px;
    }

    .flavour {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
        width: 100%;
        padding: 2%;
    }

    .flavour h1 {
        font-size: 5vw;
    }

    .flav-pic {
        height: 80vh;
        width: auto;
    }

    .flav-line {
        width: 80%;
    }

    .flav-nutritions {
        display: flex;
        flex-direction: row;
        align-items: flex-start;
        justify-content: flex-start;
    }

    .flav-nutritions p {
        padding-right: 20px;
        font-size: 3vw;
    }

    p.flav-ingredients{
        font-size: 3vw;
    }

    .flavour button {
        margin-top: 90px;
        width: 100%;
    }

    .line {
        height: 3px;
        margin: 20px 0;
    }

    .amount {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
    }

    .amount button {
        font-size: 30px;
        padding: 10px 10px;
        margin: 0 10px;
        border: none;
        background-color: #fff;
        color: #000;
        cursor: pointer;
        width: 60px;
        height: 60px;
        border-radius: 100%;
    }

    .amount p {
        border: none;
        background-color: #f7f5f4;
        cursor: pointer;
        font-size: 38px;
        padding: 10px 30px;
        border-radius: 18px;
        box-shadow: 0px 3px 5px 0px rgba(0, 0, 0, 0.75);
        margin: 20px 0;
        font-family: "montserrat", sans-serif;
        font-weight: 500;
        color: #000;
    }

    .add-to-cart button {
        border: none;
        background-color: #f7f5f4;
        cursor: pointer;
        font-size: 30px;
        padding: 10px 30px;
        border-radius: 18px;
        box-shadow: 0px 3px 5px 0px rgba(0, 0, 0, 0.75);
        margin: 20px 0;
        font-family: "montserrat", sans-serif;
        font-weight: 500;
        color: #000;
    }

    .amount-and-cart {
        display: flex;
        flex-direction: row;
    }

    .flavour-container .flavour .flav-desc {
        font-weight: 300;
    }

    .go-back {
        position: fixed;
        bottom: 20px;
        left: 20px;
        font-size: 50px;
        background-color: #fff;
        border: none;
        cursor: pointer;
        padding: 10px 20px;
        border-radius: 100%;
        box-shadow: 0px 3px 5px 0px rgba(0, 0, 0, 0.75);
        font-family: "montserrat", sans-serif;
        font-weight: 500;
        color: #000;
        height: 100px;
        width: 100px;
    }

    .flav-text {
        width: 33%;
    }
</style>