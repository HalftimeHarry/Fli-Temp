<script lang="ts">
	import VegasPopUp from '$lib/components/VegasPopUp.svelte';
	import { overlayStore } from '$lib/overlayStore';
	import Icon from '@iconify/svelte';

	let continuousText = '... Placeholder text for the ticker...';

	function toggleVegasPopUp() {
		if ($overlayStore === 'vegas') {
			overlayStore.set('');
		} else {
			overlayStore.set('vegas');
		}
	}

	function closeVegasPopUp() {
		overlayStore.set('');
	}

	function navigateTo(url) {
		window.location.href = url;
	}
</script>

<div class="container mx-auto p-4 border-t border-white z-10">
	<div
		class="top-row flex flex-row flex-wrap space-x-2 sm:space-x-4 mb-4 sm:mb-8 justify-between md:justify-start"
	>
		<!-- Main Menu Links -->
		<div class="space-x-2 sm:space-x-4 w-full sm:w-auto mb-4 sm:mb-0 md:flex">


			<button
				class="flex items-center bg-green-500 hover:bg-green-700 text-black font-extrabold py-1 px-2 rounded focus:outline-none focus:shadow-outline mb-2 w-full sm:w-auto"
				on:click={() => navigateTo('info')}
			>
				<Icon icon="carbon:information" class="mr-2" />
				<span>Information</span>
			</button>
		</div>


	</div>
</div>
