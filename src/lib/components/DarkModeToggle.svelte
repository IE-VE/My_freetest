<script lang="ts">
	// State for dark mode
	let isDarkMode = $state(false);

	// On mount, check if dark mode is already set
	$effect(() => {
		if (typeof document !== 'undefined') {
			// Check for system preference or stored preference
			const storedTheme = localStorage.getItem('theme');

			if (
				storedTheme === 'dark' ||
				(!storedTheme && window.matchMedia('(prefers-color-scheme: dark)').matches)
			) {
				document.documentElement.classList.add('dark');
				isDarkMode = true;
			} else {
				document.documentElement.classList.remove('dark');
				isDarkMode = false;
			}
		}
	});

	// Handle toggle click
	function toggleDarkMode() {
		isDarkMode = !isDarkMode;

		if (isDarkMode) {
			document.documentElement.classList.add('dark');
			localStorage.setItem('theme', 'dark');
		} else {
			document.documentElement.classList.remove('dark');
			localStorage.setItem('theme', 'light');
		}
	}
</script>

<button
	aria-label="Toggle dark mode"
	class="flex h-8 w-8 items-center justify-center rounded-md transition-colors hover:bg-gray-100 dark:hover:bg-gray-800"
	onclick={toggleDarkMode}
>
	{#if isDarkMode}
		<!-- Sun icon for light mode -->
		<svg
			xmlns="http://www.w3.org/2000/svg"
			class="h-5 w-5 text-amber-500"
			viewBox="0 0 20 20"
			fill="currentColor"
		>
			<path
				fill-rule="evenodd"
				d="M10 2a1 1 0 011 1v1a1 1 0 11-2 0V3a1 1 0 011-1zm4 8a4 4 0 11-8 0 4 4 0 018 0zm-.464 4.95l.707.707a1 1 0 001.414-1.414l-.707-.707a1 1 0 00-1.414 1.414zm2.12-10.607a1 1 0 010 1.414l-.706.707a1 1 0 11-1.414-1.414l.707-.707a1 1 0 011.414 0zM17 11a1 1 0 100-2h-1a1 1 0 100 2h1zm-7 4a1 1 0 011 1v1a1 1 0 11-2 0v-1a1 1 0 011-1zM5.05 6.464A1 1 0 106.465 5.05l-.708-.707a1 1 0 00-1.414 1.414l.707.707zm1.414 8.486l-.707.707a1 1 0 01-1.414-1.414l.707-.707a1 1 0 011.414 1.414zM4 11a1 1 0 100-2H3a1 1 0 000 2h1z"
				clip-rule="evenodd"
			/>
		</svg>
	{:else}
		<!-- Moon icon for dark mode -->
		<svg
			xmlns="http://www.w3.org/2000/svg"
			class="h-5 w-5 text-gray-700"
			viewBox="0 0 20 20"
			fill="currentColor"
		>
			<path d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z" />
		</svg>
	{/if}
</button>
