<script lang="ts">
	import { onMount } from 'svelte';
	import { onDestroy } from 'svelte';
	import logoDark from '../assets/images/logo-blk-wt.png';
	import logoLight from '../assets/images/logo-wt-blk.png';
	import Modal from './Modal.svelte';
	import { supabase } from '../supabaseClient';

	let menu = false;
	let loading = false;
	let modalTypeToShow = null; // Declare modalTypeToShow at the top level
	let isAuthenticated = false; // Track authentication state

	// Check authentication status on mount
	onMount(async () => {
		handleRouteChange();

		// Subscribe to authentication state changes
		const { data: authListener } = supabase.auth.onAuthStateChange((event, session) => {
			// Update isAuthenticated based on session presence
			isAuthenticated = session !== null;
		});

		// Initial check for authentication status
		const session = supabase.auth.session();
		isAuthenticated = session !== null;

		return () => {
			// Unsubscribe from authentication state changes when component is destroyed
			authListener.unsubscribe();
		};
	});

	const handleRouteChange = () => {
		loading = false;
	};

	function handleAnchorClick(event) {
		event.preventDefault();
		const link = event.currentTarget;
		const anchorId = new URL(link.href).hash.replace('#', '');
		const anchor = document.getElementById(anchorId);
		window.scrollTo({
			top: anchor.offsetTop,
			behavior: 'smooth'
		});
	}

	// Define openModal function
	function openModal(modalType) {
		console.log('Opening modal:', modalType); // Log a message to console
		// Set the modalTypeToShow to trigger modal display
		modalTypeToShow = modalType;
	}

	// Function to handle sign out
	async function handleSignOut() {
		try {
			loading = true;
			const { error } = await supabase.auth.signOut();
			if (error) throw error;
			// Update authentication state after sign out
			isAuthenticated = false;
		} catch (error) {
			console.error('Sign out error:', error.message);
		} finally {
			loading = false;
		}
	}
</script>

<Modal {modalTypeToShow} />
<!-- Render the Modal component with modalType prop -->

<nav class="navbar" id="navbar">
	<div class="container relative flex flex-wrap items-center justify-between">
		<a class="navbar-brand md:me-8" href="/">
			<img src={logoDark} class="inline-block dark:hidden" alt="" />
			<img src={logoLight} class="hidden dark:inline-block" alt="" />
		</a>
	</div>
</nav>
