<script lang="ts">
	import Sidebar from './Sidebar.svelte';
	import Header from './Header.svelte';

	let { children, title }: { children: any; title?: string } = $props();
</script>

<div class="h-screen flex bg-slate-50">
	<Sidebar />

	<div class="flex-1 flex flex-col min-w-0">
		<Header {title} />

		<main class="flex-1 overflow-auto p-6">
			{@render children()}
		</main>
	</div>
</div>
