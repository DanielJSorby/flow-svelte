<script>
    import '/src/global.css';
    import Navbar from '../../Components/nabar.svelte';
    let cart = [];

    if (typeof window !== 'undefined') {
        cart = JSON.parse(localStorage.getItem('cart') || '[]');
    }

    function increaseAmount(item) {
        const index = cart.indexOf(item);
        cart[index].amount++;
    }

    function decreaseAmount(item) {
        const index = cart.indexOf(item);
        if (cart[index].amount > 0) {
            cart[index].amount--;
        }
    }

    function clearCart() {
        if (typeof window !== 'undefined') {
            cart = [];
            localStorage.setItem('cart', JSON.stringify(cart));
        }
    }

    let totalPrice = 0;

    $: totalPrice = cart.reduce((total, item) => total + item.price * item.amount, 0);
</script>

<Navbar />
<div class="body">
    <div class="name-and-total">
        <h1>Your Cart</h1>
        <h2>Total Price: $ {totalPrice}.00</h2>
    </div>
    <div class="cart-items">
        {#each cart as item (item.name)}

            <div class="cart-item">
                <div class="image-and-price-name">
                    <img src="{item.image}" alt={item.name} />
                    <div class="name-and-price">
                        <h2>{item.name}</h2>
                        <p class="price">$ {item.price}.00</p>
                    </div>
                </div>
                <div class="amount">
                    <button on:click={() => decreaseAmount(item)}>-</button>
                    <p>{item.amount}</p>
                    <button on:click={() => increaseAmount(item)}>+</button>
                </div>
            </div>
            <div class="line"></div>
        {/each}
    </div>
    <button on:click={clearCart}>Clear Cart</button>
</div>

<style>
    .body {
        background-color: #454C5F;
        height: 100%;
        color: #454C5F;
        padding-top: 20vh;
    }

    .line {
        width: 80%;
        height: 4px;
        background-color: #454C5F;
        margin: 0 auto;
    }
    .price {
        font-size: 20px;
    }

    img {
        height: 10vh;
        width: auto;
    }

    .cart-items {
        display: flex;
        justify-content: center;
        flex-direction: column;
        background-color: #FFFFFF;
        width: 80%;
        margin: 0 auto;
        border-radius: 42px;
        padding: 40px;
    }

    .name-and-total {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: flex-end;
        color: #FFFFFF;
        width: 80%;
        padding: 2px 20px;
        margin: 0 auto;
    }

    .name-and-price {
        padding: 20px;
    }

    .cart-item {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
        width: 100%;
        margin: 20px;
    }

    .image-and-price-name {
        display: flex;
        flex-direction: row;
    }
    
    .amount {
        display: flex;
        flex-direction: row;
        align-items: center;
        font-size: 40px;
    }

    .amount p {
        font-size: 40px;
    }

    .amount button {
        height: 5vh;
        width: 5vh;
        padding: 0;
        margin: 12px;
    }

    .amount button:hover {
        background-color: #666F88;
        color: #f7f5f4;
    }
</style>