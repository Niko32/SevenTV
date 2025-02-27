<script lang="ts">
	import HideOn from "$/components/hide-on.svelte";
	import SearchBar from "$/components/nav/search-bar.svelte";
	import PaintPreview from "$/components/paint-preview.svelte";
	import Select from "$/components/select.svelte";
	import Banner from "$/components/store/banner.svelte";
	import { faGift, faCartShopping } from "@fortawesome/pro-regular-svg-icons";
	import { faSearch } from "@fortawesome/pro-solid-svg-icons";
	import Fa from "svelte-fa";

	const bundles = [
		{
			name: "Summer Bundle",
			price: 199,
			new: true,
		},
		{
			name: "Winter Bundle",
			price: 500,
			new: false,
		},
		{
			name: "Halloween Bundle",
			price: 299,
			new: false,
		},
		{
			name: "Loser Bundle",
			price: 1,
			new: false,
		},
		{
			name: "Random Bundle",
			price: 199,
			new: false,
		},
		{
			name: "Forsen Bundle",
			price: 1099,
			new: false,
			oldPrice: 10099,
		},
	];

	const priceFormat = new Intl.NumberFormat("en-US", {
		style: "currency",
		currency: "USD",
	});
</script>

<svelte:head>
	<title>Paint Bundles - 7TV</title>
</svelte:head>

<Banner title="Make Yourself Glow" subtitle="Nametag Paints Will Let You Express Yourself in Every Hue." gradientColor="#27cfb1" />
<section>
	<div class="header">
		<h2>Paint Bundles</h2>
		<div class="buttons">
			<HideOn mobile>
				<SearchBar />
			</HideOn>
			<button class="button square hide-on-desktop">
				<Fa icon={faSearch} size="1.2x" fw />
			</button>
			<Select options={["Filters"]} />
		</div>
	</div>
	<div class="grid">
		{#each bundles as bundle}
			<div class="bundle">
				<div class="header">
					<span class="name">{bundle.name}</span>
					{#if bundle.new}
						<span class="new">NEW</span>
					{/if}
				</div>
				{#each Array(3) as _}
					<PaintPreview />
				{/each}
				<div class="buttons">
					<button class="button secondary icon-left">
						<Fa icon={faGift} size="1.2x" />
						Gift
					</button>
					<button class="button secondary icon-left">
						<Fa icon={faCartShopping} size="1.2x" />
						<span>
							{#if bundle.oldPrice}
								<del>{priceFormat.format(bundle.oldPrice / 100)}</del>
							{/if}
							{priceFormat.format(bundle.price / 100)}
						</span>
					</button>
				</div>
			</div>
		{/each}
	</div>
</section>

<style lang="scss">
	section {
		margin-top: 1rem;
		margin-inline: auto;
		max-width: 80rem;
	}

	h2 {
		font-size: 1.25rem;
		font-weight: 700;
	}

	.header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		gap: 0.5rem;

		.buttons {
			display: flex;
			gap: 0.5rem;
			align-items: center;
		}
	}

	.grid {
		margin-top: 1rem;

		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(20rem, 1fr));
		gap: 1rem;
	}

	.bundle {
		padding: 1rem 1.25rem;
		display: flex;
		flex-direction: column;
		gap: 1rem;
		background-color: var(--bg-medium);
		border-radius: 0.5rem;

		.header {
			display: flex;
			justify-content: space-between;
			align-items: center;

			.name {
				font-weight: 500;
			}

			.new {
				color: var(--subscriber-accent);
				border: 1px solid var(--subscriber-accent);
				padding: 0.2rem 0.5rem;
				border-radius: 0.25rem;
				font-size: 0.625rem;
			}
		}

		.buttons {
			display: flex;
			gap: 0.5rem;
			justify-content: flex-end;
		}

		del {
			font-size: 0.75rem;
		}
	}
</style>
