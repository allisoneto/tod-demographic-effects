<script>
	import { base } from '$app/paths';
	import { page } from '$app/state';

	// Use route id so active states work when kit.paths.base is set (e.g. GitHub Pages).
	const onPoc = $derived(page.route.id === '/');
	const onIncomeTod = $derived(page.route.id === '/income-tod');
	const onTract = $derived(page.route.id === '/tract');
	const onPolicy = $derived(page.route.id === '/policy');
	const onDevTools = $derived(onIncomeTod || onTract || onPolicy);

	let devToolsOpen = $state(false);

	$effect(() => {
		page.url.pathname;
		devToolsOpen = false;
	});
</script>

<nav class="navbar" aria-label="Primary">
	<a class="brand" href="{base}/">TOD Demographics Dashboard</a>
	<ul class="links">
		<li>
			<a href="{base}/" class:active={onPoc}>POC</a>
		</li>
		<li class="dropdown-wrap">
			<details class="dev-tools" bind:open={devToolsOpen}>
				<summary class="dev-tools__summary" class:dev-tools__summary--active={onDevTools}>
					Dev Tools
				</summary>
				<ul class="dev-tools__menu">
					<li>
						<a href="{base}/income-tod" class:active={onIncomeTod}>Income &amp; TOD</a>
					</li>
					<li>
						<a href="{base}/tract" class:active={onTract}>Tract dashboard</a>
					</li>
					<li>
						<a href="{base}/policy" class:active={onPolicy}>Policy insights</a>
					</li>
				</ul>
			</details>
		</li>
	</ul>
</nav>

<style>
	.navbar {
		position: sticky;
		top: 0;
		z-index: 100;
		display: flex;
		align-items: center;
		justify-content: space-between;
		height: 56px;
		padding: 0 20px;
		background: var(--bg-panel);
		border-bottom: 1px solid var(--border);
		box-shadow: var(--shadow);
	}

	.brand {
		font-weight: 600;
		font-size: 1rem;
		color: var(--text);
		letter-spacing: -0.02em;
	}

	.brand:hover {
		color: var(--accent-hover);
	}

	.links {
		display: flex;
		align-items: center;
		gap: 8px;
		list-style: none;
		margin: 0;
		padding: 0;
	}

	.links > li > a,
	.dev-tools__summary {
		display: inline-flex;
		align-items: center;
		gap: 6px;
		padding: 8px 14px;
		border-radius: var(--radius-sm);
		color: var(--text-muted);
		font-size: 0.9375rem;
		transition:
			background 0.15s ease,
			color 0.15s ease;
	}

	.links > li > a:hover,
	.dev-tools__summary:hover {
		color: var(--text);
		background: var(--bg-hover);
	}

	.links > li > a.active {
		color: var(--accent);
		background: color-mix(in srgb, var(--accent) 12%, transparent);
	}

	.dropdown-wrap {
		position: relative;
	}

	.dev-tools {
		position: relative;
	}

	.dev-tools__summary {
		list-style: none;
		cursor: pointer;
		user-select: none;
		font: inherit;
		border: 1px solid transparent;
	}

	.dev-tools__summary::-webkit-details-marker {
		display: none;
	}

	.dev-tools__summary::after {
		content: '';
		display: inline-block;
		width: 0;
		height: 0;
		border-left: 4px solid transparent;
		border-right: 4px solid transparent;
		border-top: 5px solid currentColor;
		opacity: 0.65;
		margin-top: 2px;
		transition: transform 0.15s ease;
	}

	.dev-tools[open] .dev-tools__summary::after {
		transform: rotate(180deg);
		margin-top: -2px;
	}

	.dev-tools__summary--active:not(:hover) {
		color: var(--accent);
		background: color-mix(in srgb, var(--accent) 12%, transparent);
		border-color: color-mix(in srgb, var(--accent) 35%, var(--border));
	}

	.dev-tools__menu {
		position: absolute;
		top: calc(100% + 6px);
		right: 0;
		min-width: 12rem;
		margin: 0;
		padding: 6px;
		list-style: none;
		background: var(--bg-card);
		border: 1px solid var(--border);
		border-radius: var(--radius-sm);
		box-shadow: var(--shadow);
		z-index: 200;
	}

	.dev-tools__menu a {
		display: block;
		padding: 8px 12px;
		border-radius: var(--radius-sm);
		color: var(--text-muted);
		font-size: 0.9375rem;
		text-decoration: none;
		transition:
			background 0.15s ease,
			color 0.15s ease;
	}

	.dev-tools__menu a:hover {
		color: var(--text);
		background: var(--bg-hover);
	}

	.dev-tools__menu a.active {
		color: var(--accent);
		background: color-mix(in srgb, var(--accent) 12%, transparent);
	}
</style>
