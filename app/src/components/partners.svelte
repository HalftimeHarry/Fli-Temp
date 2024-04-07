<!-- Partners.svelte -->

<script>
	import par1lt from '../assets/images/partners/pure_lt.png';
	import par1dk from '../assets/images/partners/pure_dk.png';
	import par2main from '../assets/images/partners/ame_main_logo.webp';
</script>

<div class="bg-white py-6 sm:py-8 lg:py-12">
	<div class="mx-auto max-w-screen-2xl px-4 md:px-8">
		<div class="mb-4 flex flex-col items-center md:mb-8 lg:flex-row lg:justify-between">
			<h2 class="mb-2 text-center text-2xl font-bold text-gray-800 lg:mb-0 lg:text-3xl">
				Trusted by the best
			</h2>

			<p class="max-w-md text-center text-gray-400 lg:text-right">
				Filler text is dummy text which has no meaning however looks very similar to real text.
			</p>
		</div>

		<div class="grid grid-cols-2 gap-4 rounded-lg md:grid-cols-3 lg:gap-6">
			<!-- Partner logos -->
			<div
				class="flex h-16 items-center justify-center rounded-lg bg-gray-100 p-4 text-gray-400 sm:h-32"
			>
				<img src={par1lt} alt="Partner 1 Logo" />
			</div>

			<div
				class="flex h-16 items-center justify-center rounded-lg bg-gray-100 p-4 text-gray-400 sm:h-32"
			>
				<img src={par1dk} alt="Partner 2 Logo" />
			</div>

			<div
				class="flex h-16 items-center justify-center rounded-lg bg-gray-100 p-4 text-gray-400 sm:h-32"
			>
				<img src={par2main} alt="Partner 3 Logo" />
			</div>
			<!-- Add more partner logos as needed -->
		</div>
	</div>
</div>
