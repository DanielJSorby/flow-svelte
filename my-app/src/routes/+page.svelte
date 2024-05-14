<script>
    import Navbar from '../Components/nabar.svelte';
    import '/src/global.css';
</script>


<Navbar linkColor={"#7f8491"}/>
<div class="start-home" style="margin-bottom: 200vh;">
    <div class="slogan-and-button">
        <div class="slogan">
            <h1>Enter <br>Your <span class="text-light-blue">Zone.</span></h1>
        </div>
        <div class="bottles-container">
            <img src="src/images/Bottles/Cadoflower+.png" alt="A bottle of the flavour Cadoflower" class="bottle" id="bottle1">
            <img src="src/images/Bottles/Bloody Ginger.png" alt="A bottle of the flavour Bloody Ginger" class="bottle" id="bottle2">
        </div>
    </div>
    <a href="./Flavours/">
        <button id="home-button">Our Products</button>
    </a>
</div>

<style>
    .start-home {
        background: linear-gradient(
            73deg,
            rgba(69, 76, 95, 1) 70%,
            rgba(247, 245, 244, 1) 70%
        );
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
        height: 100vh;
        padding: 0 40px;
    }

    .slogan-and-button {
        width: 100%;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
    }

    .start-home .slogan {
        text-shadow: 2px 2px #000000;
    }

    .bottle {
        width: auto;
        height: 80vh;
    }

    #bottle1 {
        position: absolute;
        rotate: 40deg;
        right: 70px;
        top: 12vh;
    }

    #bottle2 {
        position: absolute;
        top: 12vh;
        right: 300px;
    }

    #home-button {
        position: absolute;
        right: 0;
        bottom: 30px;
        background-color: #666F88;
        color: #f7f5f4;
    }
</style>