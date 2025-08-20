<script lang="ts">
  import { supabase } from '$lib/supabaseClient';
  let email = '';
  let password = '';
  let message = '';

  const signUp = async () => {
    const { error } = await supabase.auth.signUp({
      email,
      password,
      options: { emailRedirectTo: import.meta.env.VITE_SUPABASE_REDIRECT_URL }
    });
    message = error ? error.message : 'Check your email to confirm your account.';
  };
</script>

<form on:submit|preventDefault={signUp}>
  <input type="email" bind:value={email} placeholder="Email" required />
  <input type="password" bind:value={password} placeholder="Password" required />
  <button type="submit">Sign Up</button>
</form>

{#if message}<p>{message}</p>{/if}
