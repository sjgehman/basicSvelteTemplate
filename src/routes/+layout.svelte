<script lang="ts">
  import Header from "$lib/components/Header.svelte";
  import "../app.css";
  import { ModeWatcher } from "mode-watcher";
  let { children } = $props();
</script>

<ModeWatcher />
<Header />

<main class="container mx-auto p-4">
  {@render children?.()}
</main>