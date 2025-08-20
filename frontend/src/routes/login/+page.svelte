<script lang="ts">
  import { supabase } from '$lib/supabaseClient';
  import OAuthButtons from '$lib/components/OAuthButtons.svelte';
  let email = '';
  let message = '';

  const sendMagicLink = async () => {
    const { error } = await supabase.auth.signInWithOtp({
      email,
      options: { emailRedirectTo: import.meta.env.VITE_SUPABASE_REDIRECT_URL }
    });
    message = error ? error.message : 'Check your email for a magic link to log in.';
  };
</script>

<form on:submit|preventDefault={sendMagicLink}>
  <input type="email" bind:value={email} placeholder="Email" required />
  <button type="submit">Send Magic Link</button>
</form>

<OAuthButtons />

{#if message}<p>{message}</p>{/if}
