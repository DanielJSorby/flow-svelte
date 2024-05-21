<style>
    .navbar {
	display: flex;
	justify-content: space-between;
	align-items: center;
	color: #11161c;
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	font-size: 35px;
    }

    #nav-name {
        font-size: 60px;
        padding-left: 20px;
        text-shadow: 2px 2px 5px rgba(0,0,0,0.54);
    }

    .nav-links {
        display: flex;
        flex-direction: row;
    }

    .navbar .nav-links a {
        color: #454c5f;
        text-decoration: none;
        margin: 0 20px;
        font-weight: 300;
    }

    #nav-about {
        font-weight: 300;
    }

    .navbar li {
        list-style: none;
    }
</style>

<div class="navbar" style="height: {navHeight}px;">
    <div class="logo-contaier">
        <a href="../" class="text-white no-style">
            <!-- <img src="./images/Logo/Logo-white-bold.png" alt="Logo" class="logo" id="navbar-logo"> -->
            <h1 class="text-white no-style" id="nav-name" style="color: {color}">Flow</h1>
        </a>
    </div>
    <ul class="nav-links">
        <li><a href="./cart/" style="color: {linkColor}">Cart</a></li>
        <li><a href="about.html" id="nav-about" style="color: {linkColor}">About</a></li>
</div>

<script>
    import { onMount } from 'svelte';
    
    export let changeColor = false;
    let navHeight = 117

    export let color = '#fff';
    export let linkColor = color;
    /* const allFlavours = document.getElementById('all-flavours'); */

    onMount(() => {
        if (changeColor) {
            const handleScroll = () => {
                const scrollHeight = window.pageYOffset + navHeight/2 ;
                const windowHeight = window.innerHeight;

                if (scrollHeight < windowHeight) {
                    color = '#fff';
                    linkColor = color;
                    console.log('top');
                } else if (scrollHeight < 2 * windowHeight) {
                    color = '#6A8C65';
                    linkColor = color;
                    console.log('middle');
                } else if (scrollHeight < 3 * windowHeight) {
                    color = '#FFFABA';
                    linkColor = color;
                    console.log('bottom');
                }
            };

            window.addEventListener('scroll', handleScroll);

            return () => {
                window.removeEventListener('scroll', handleScroll);
            };
        }
    });

</script>
