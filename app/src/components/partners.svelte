<!-- Partners.svelte -->

<script>
	import win_logo from '../assets/images/partners/winmo_logo.svg';
	import pure_logo from '../assets/images/partners/pure_lt.png';
	import ame_logo from '../assets/images/partners/ame_main_logo.webp';

	// Variable to track the toggle state
	let isDarkMode = false;

	// Function to toggle dark mode
	function toggleDarkMode() {
		isDarkMode = !isDarkMode;
	}
</script>

<!-- Apply conditional classes based on the toggle state -->
<div
	class="{isDarkMode
		? 'bg-gray-900 text-white'
		: 'bg-white text-gray-800'} py-6 sm:py-8 lg:py-12 relative"
>
	<!-- Toggle button for dark mode -->
	<button
		class="absolute top-4 right-4 px-3 py-1 bg-gray-900 text-white rounded"
		on:click={toggleDarkMode}
	>
		{isDarkMode ? 'Light Mode' : 'Dark Mode'}
	</button>

	<div class="mx-auto max-w-4xl px-4 md:px-8">
		<!-- Increased the container size to max-w-4xl -->
		<!-- Row for "Trusted by the best" -->
		<div class="mb-4">
			<h2 class="mb-2 text-center text-2xl font-bold lg:mb-0 lg:text-3xl">Trusted by the best</h2>
		</div>

		<!-- Row for "Filler text is dummy text..." -->
		<div class="mb-4">
			<p class="max-w-md mx-auto text-center lg:max-w-xl">
				<!-- Centering the paragraph and setting max width -->
				Partners
			</p>
		</div>

		<!-- Grid for partner logos -->
		<div class="grid grid-cols-1 gap-4 rounded-lg md:grid-cols-2 lg:gap-6">
			<!-- Changed grid-cols to 1 for mobile, 2 for medium screens and centering the images -->
			<!-- Partner logos -->
			<div
				class="flex h-16 items-center justify-center rounded-lg bg-gray-100 p-4 text-gray-400 sm:h-32"
			>
				<img src={pure_logo} alt="Partner 1 Logo" />
			</div>

			<div
				class="flex h-16 items-center justify-center rounded-lg bg-gray-100 p-4 text-gray-400 sm:h-32"
			>
				<img src={win_logo} alt="Partner 1 Logo" />
			</div>

			<div
				class="flex h-16 items-center justify-center rounded-lg bg-gray-100 p-4 text-gray-400 sm:h-32"
			>
				<img src={ame_logo} alt="Partner 3 Logo" />
			</div>
			<!-- Add more partner logos as needed -->
		</div>
	</div>
</div>
