<script lang="ts">
	import Counter from './Counter.svelte';
	import wartenummerImg from '$lib/images/wartenummer.png';
				
	let counter = 0;	
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Wartenummer" />
</svelte:head>

<section>
	<h1>
		<span class="welcome">
			<picture>
				<source srcset={wartenummerImg} type="image/webp" />
				<img src={wartenummerImg} alt="DressedMonkeyImg" />
 			</picture>
		</span>
	</h1>

	<h2>
		Bitte Nummer ziehen	
	</h2>

	<Counter count={counter} />

	<input type="button" value="Ziehen" on:click={() => {counter++}} />
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}

	.wartenummerImg {
		display: block;
		position: relative;
		width: 100%;
		height: 0;
	}

	.wartenummerImg img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}
</style>
