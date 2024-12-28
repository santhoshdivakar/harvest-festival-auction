<script>
	import { onMount } from 'svelte';
	import { navigate, Route, Router, Link } from 'svelte-routing';
	import Home from './Home.svelte';
	import Login from './Login.svelte';
	import NewItem from './components/NewItem.svelte';
	import Auction from './components/Auction.svelte';
	//onMount(() => {
	//	navigate('/home', { replace: true });
	//});
</script>

<main>
	
	
	<Router>
		<nav class="navbar">
			<Link to="/">Home</Link>
			<Link to="/login">Login</Link>
		</nav>
		
		<Route path="/" component={Home} />
		<Route path="/login" component={Login} />
		<Route path="/newItem" component={NewItem} />
		<Route path="/auction" component={Auction} />
	</Router>
</main>

<style>
	.navbar {
		display: flex;
		background-color: #777;
		justify-content: space-between;
		padding: 1em;
	}

	.navbar {
		color: #f2f2f2;
		text-decoration: none;
		padding: 0.5em;
	}
</style>