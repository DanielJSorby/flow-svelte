<script>
	import { selectedFlavour } from '../lib/store';
    /* import { onMount } from 'svelte'; */
    function setFlavour(newFlavour) {
        $selectedFlavour = newFlavour; // Update the store
    }
    let flavours = [{
		"name": "Cadoflower+",
		"price": 3.00,
		"currency": "$",
		"image": "images/Bottles/Cadoflower+.png",
		"mainColor": "#6A8C65",
		"secondColor": "#FFFFFF",
		"ingredients": ["Avocado", "Elderflower"],
		"coffeine": "105mg",
		"vitamin": "70mcg",
		"vitaminType": "K",
		"description": "Carefully crafted to ensure quality in every drop. Based on the daring depths of South America and Innovative ends in Europe inspiring exploration and development."
	},

	{
		"name": "Minty Citrus",
		"price": 3,
		"currency": "$",
		"image": "images/Bottles/Minty Citrus.png",
		"mainColor": "#FFFABA",
		"secondColor": "#6A8C65",
		"ingredients": ["Mint", "Lemon"],
		"coffeine": "105mg",
		"vitamin": "70mcg",
		"vitaminType": "C",
		"description": "Meticulously crafted to deliver an unforgettable taste experience. Inspired by the lush orchards of the Mediterranean and the invigorating coolness of Alpine peaks, this blend takes your taste buds on a journey of discovery and delight."
	},

	{
		"name": "Bloody Ginger",
		"price": 3,
		"currency": "$",
		"image": "images/Bottles/Bloody Ginger.png",
		"mainColor": "#FFBC98",
		"secondColor": "#FFFABA",
		"ingredients": ["Blood Orange", "Ginger"],
		"coffeine": "105mg",
		"vitamin": "250mcg",
		"vitaminType": "K",
		"description": "Crafted with attention to detail to deliver an unparalleled taste experience. Inspired by the sun-drenched orchards of Sicily and the rugged beauty of the Australian Outback, this blend offers a tantalizing journey of flavor exploration."
	}];

	if (typeof window !== 'undefined') {
        localStorage.setItem('flavours', JSON.stringify(flavours));
    }

    /* async function fetchFlavours() {
        const response = await fetch("../lib/flavours.json"); 
        const data = await response.json();
        flavours = data;
        console.log(flavours)
    }

    onMount(async () => {
    fetchFlavours();
}); */
</script>
<div class="all-flavours" id="all-flavours">
{#each flavours as flavour (flavour.name)}
    <div class="flavour-container {flavour.name}" style="background-color: {flavour.mainColor}; color: {flavour.secondColor}">
        <div class="flavour">
            <div class="flav-text-button">
                <div class="flav-text">
                    <h1 class="flav-name">{flavour.name}</h1>
                    <div class="flav-desc">
                        <p class="flav-ingredients">
                            {@html flavour.ingredients ? flavour.ingredients.join('<br>') : 'No ingredients listed'}
                        </p>
                        <div class="line flav-line" style="background-color: {flavour.secondColor}"></div>
                        <div class="flav-nutritions">
                            <p class="flav-numbers">{flavour.coffeine}<br>{flavour.vitamin}</p>
                            <p class="flav-names">Coffeine<br>Vitamin {flavour.vitaminType}</p>
                        </div>
                    </div>
                </div>
                <!-- <a href="Flavours/{flavour.name}/"> -->
					<div class="flav-button" style="background-color: {flavour.mainColor};">
						<button on:click={() => setFlavour(flavour.name)}>Purchase</button>
					</div>
				<!-- </a> -->
            </div>
            <div class="flav-image">
                <img src="{flavour.image}" alt="{flavour.name}" class="flav-pic">
            </div>
        </div>
    </div>
{/each}
</div>
<style>
.all-flavours {
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

.flavour {
	display: flex;
	flex-direction: row;
	align-items: center;
	justify-content: space-evenly;
	width: 100%;
}

.flavour h1 {
	font-size: 80px;
}

.flav-pic {
	height: 80vh;
	width: auto;
}

.flav-line {
	width: 80%;
}

.flavour p {
	font-size: 50px;
	font-weight: 600;
}

.flav-nutritions {
	display: flex;
	flex-direction: row;
	align-items: flex-start;
	justify-content: flex-start;
}

.flav-nutritions p {
	padding-right: 20px;
}

.flavour button {
	margin-top: 90px;
	width: 100%;
}

.line {
	height: 3px;
	margin: 20px 0;
}
</style>