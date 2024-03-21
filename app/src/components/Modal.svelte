<script>
  import Auth from '$lib/Auth.svelte'; // Import Auth component
  import authStore from '../lib/AuthStore';
  import { onMount } from 'svelte';

  let showModal = false;
  let activeTab = 'register';

  onMount(() => {
    // Initialize the formType in the authStore
    authStore.set({ formType: 'register' });
  });

  // Subscribe to changes in the authStore
  authStore.subscribe((state) => {
    // Set showModal based on the presence of formType
    showModal = !!state.formType;
    // Set activeTab based on formType
    activeTab = state.formType || 'register';
  });

  // Function to close the modal
  export function closeModal() {
    authStore.set({ formType: null }); // Reset formType to close the modal
  }

  // Function to open the register form
  function openRegisterForm() {
    authStore.set({ formType: 'register' });
  }

  // Function to open the login form
  function openLoginForm() {
    authStore.set({ formType: 'login' });
  }
</script>

<!-- Render the modal if showModal is true -->
{#if showModal}
  <div class="fixed inset-0 z-50 flex items-center justify-center bg-black bg-opacity-50">
    <div class="bg-white p-6 rounded-lg shadow-lg max-w-md relative">
      <!-- Tabs for switching between register and login -->
      <div class="tabs">
        <!-- Button to switch to register form -->
        <button class="tab" class:selected={activeTab === 'register'} on:click={openRegisterForm}>Register</button>
        <!-- Button to switch to login form -->
        <button class="tab" class:selected={activeTab === 'login'} on:click={openLoginForm}>Login</button>
      </div>
      <!-- Render register form if activeTab is 'register' -->
      {#if activeTab === 'register'}
        <Auth formType="register" on:close={closeModal} />
      {:else if activeTab === 'login'}
        <!-- Render login form if activeTab is 'login' -->
        <Auth formType="login" on:close={closeModal} />
      {/if}
    </div>
  </div>
{/if}

<!-- Add your existing styles here -->
<style>
  /* Modal styles */
  .modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 9999;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal {
    background-color: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }

  .tabs {
    display: flex;
    margin-bottom: 1rem;
  }

  .tab {
    cursor: pointer;
    padding: 0.5rem 1rem;
    border: none;
    background-color: transparent;
    color: #333;
    font-size: 1rem;
    border-radius: 0.25rem 0.25rem 0 0;
  }

  .tab:selected {
    background-color: #e2e8f0;
  }

  /* Update button styling */
  button {
    background-color: #4CAF50; /* Green */
    border: none;
    color: white;
    padding: 10px 20px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
    border-radius: 5px;
  }
</style>
