<script lang="ts">
	import { onMount } from 'svelte';
	import type { AuthSession } from '@supabase/supabase-js';
	import { supabase } from '/src/suprabaseClient.ts';
	import Avatar from './Avatar.svelte';

	export let session: AuthSession;

	let loading = false;
	let username: string | null = null;
	let website: string | null = null;
	let avatarUrl: string | null = null;
	let user = null; // Set the user to null initially

	onMount(() => {
		getProfile();
	});

	const getProfile = async () => {
		try {
			loading = true;
			const { user: sessionUser } = session;

			const { data, error, status } = await supabase
				.from('profiles')
				.select('username, website, avatar_url, role')
				.eq('id', sessionUser.id)
				.single();

			if (error && status !== 406) throw error;

			if (data) {
				username = data.username;
				website = data.website;
				avatarUrl = data.avatar_url;
				user = data; // Store the whole user object
			}
		} catch (error) {
			if (error instanceof Error) {
				alert(error.message);
			}
		} finally {
			loading = false;
		}
	};

	const updateProfile = async () => {
		try {
			loading = true;
			const { user: sessionUser } = session;

			const updates = {
				id: sessionUser.id,
				username,
				website,
				avatar_url: avatarUrl,
				updated_at: new Date().toISOString()
			};

			let { error } = await supabase.from('profiles').upsert(updates);

			if (error) {
				throw error;
			}
		} catch (error) {
			if (error instanceof Error) {
				alert(error.message);
			}
		} finally {
			loading = false;
			console.log('loading state: ', loading); // add this
		}
	};
</script>

<form on:submit|preventDefault={updateProfile} class="form-widget">
	<Avatar bind:url={avatarUrl} size={150} on:upload={updateProfile} />
	<div>Email: {session.user.email}</div>
	<div>
		<label for="username">Name</label>
		<input id="username" type="text" class="text-black" bind:value={username} />
	</div>
	<div>
		<label for="website">Website</label>
		<input id="website" type="text" class="text-black" bind:value={website} />
	</div>
	<div>
		<button type="submit" class="button primary block" disabled={loading}>
			{loading ? 'Saving ...' : 'Update profile'}
		</button>
	</div>
	<button type="button" class="button block" on:click={() => supabase.auth.signOut()}>
		Sign Out
	</button>
</form>
