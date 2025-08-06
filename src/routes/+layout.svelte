<script lang="ts">
	import '@gleich/ui/styles.css';
	import '../styles/fonts.css';
	import '../styles/global.css';

	import type { Snippet } from 'svelte';
	import { Layout, siteName } from '@gleich/ui';

	siteName.set('split.mattglei.ch');

	const { children }: { children: Snippet } = $props();
</script>

<Layout repo="gleich/ui">
	{@render children()}
</Layout>
