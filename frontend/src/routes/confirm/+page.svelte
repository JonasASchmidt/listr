<script lang="ts">
  import { onMount } from 'svelte';
  import { supabase } from '$lib/supabaseClient';
  import { page } from '$app/stores';
  let message = 'Confirming...';

  onMount(async () => {
    const code = $page.url.searchParams.get('code');
    if (code) {
      const { error } = await supabase.auth.exchangeCodeForSession(code);
      message = error ? error.message : 'Email confirmed! You can close this window.';
    } else {
      message = 'No confirmation code found.';
    }
  });
</script>

<p>{message}</p>
