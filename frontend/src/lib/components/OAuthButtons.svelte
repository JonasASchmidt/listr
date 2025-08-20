<script lang="ts">
  import { supabase } from '$lib/supabaseClient';

  const signInWithProvider = async (provider: 'github' | 'google') => {
    await supabase.auth.signInWithOAuth({ provider, options: { redirectTo: import.meta.env.VITE_SUPABASE_REDIRECT_URL } });
  };
</script>

<button on:click={() => signInWithProvider('github')}>Sign in with GitHub</button>
<button on:click={() => signInWithProvider('google')}>Sign in with Google</button>
