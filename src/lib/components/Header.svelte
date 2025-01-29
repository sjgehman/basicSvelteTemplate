<script lang="ts">
    import Sun from "lucide-svelte/icons/sun";
    import Moon from "lucide-svelte/icons/moon";
    import Github from "lucide-svelte/icons/github";

    import { resetMode, setMode } from "mode-watcher";
    import * as DropdownMenu from "$lib/components/ui/dropdown-menu/index.js";
    import { buttonVariants } from "$lib/components/ui/button/index.js";

    let isMenuOpen = false;
    import { onMount } from "svelte";

    let bodyBackgroundColor = "";

    onMount(() => {
        bodyBackgroundColor = getComputedStyle(document.body).backgroundColor;
    });

    function toggleMenu() {
        isMenuOpen = !isMenuOpen;
    }

    function closeMenu() {
        isMenuOpen = false;
    }
</script>

<header
    class="text-header-foreground border-b border-gray-300 dark:border-gray-700"
    style="background-color: hsl(var(--header-background));"
>
    <nav class="container mx-auto px-4 py-4 flex justify-between items-center">
        <!-- Desktop Menu -->
        <ul class="hidden md:flex space-x-6">
            <li><a href="/" class="hover:text-gray-300 font-bold">Home</a></li>
            <li><a href="#" class="hover:text-gray-300 font-bold">About</a></li>
            <li><a href="#" class="hover:text-gray-300 font-bold">Contact</a></li>
        </ul>

        <!-- Mobile Hamburger Menu -->
        <button
            class="md:hidden focus:outline-none"
            on:click={toggleMenu}
            aria-label="Toggle Menu"
        >
            <svg
                class="w-6 h-6"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
                stroke-width="2"
            >
                <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="M4 6h16M4 12h16m-7 6h7"
                />
            </svg>
        </button>

        <!-- Right Icons -->
        <div class="relative flex items-center space-x-4">
            <a href="https://github.com/sjgehman" target="_blank" rel="noopener noreferrer">
                <Github class="h-[1.2rem] w-[1.2rem] text-header-foreground" />
                <span class="sr-only">GitHub</span>
            </a>
            <DropdownMenu.Root>
                <DropdownMenu.Trigger class="relative flex items-center justify-center h-[1.2rem] w-[1.2rem]">
                    <div class="relative h-[1.2rem] w-[1.2rem]">
                        <Sun
                            class="absolute h-full w-full transition-transform transform rotate-0 scale-100 dark:-rotate-90 dark:scale-0 text-header-foreground"
                        />
                        <Moon
                            class="absolute h-full w-full transition-transform transform rotate-90 scale-0 dark:rotate-0 dark:scale-100 text-header-foreground"
                        />
                    </div>
                    <span class="sr-only">Toggle theme</span>
                </DropdownMenu.Trigger>
                <DropdownMenu.Content align="end">
                    <DropdownMenu.Item onclick={() => setMode("light")}>
                        Light
                    </DropdownMenu.Item>
                    <DropdownMenu.Item onclick={() => setMode("dark")}>
                        Dark
                    </DropdownMenu.Item>
                    <DropdownMenu.Item onclick={() => resetMode()}>
                        System
                    </DropdownMenu.Item>
                </DropdownMenu.Content>
            </DropdownMenu.Root>
        </div>
    </nav>

    <!-- Mobile Dropdown Menu -->
    {#if isMenuOpen}
        <ul
            class="md:hidden text-header-foreground"
            style="background-color: hsl(var(--header-background));"
        >
            <li>
                <a href="/" class="block px-4 py-2 hover:bg-muted hover:text-muted-foreground font-bold" on:click={closeMenu}
                    >Home</a
                >
            </li>
            <li>
                <a href="#" class="block px-4 py-2 hover:bg-muted hover:text-muted-foreground font-bold" on:click={closeMenu}
                    >About</a
                >
            </li>
            <li>
                <a href="#" class="block px-4 py-2 hover:bg-muted hover:text-muted-foreground font-bold" on:click={closeMenu}
                    >Contact</a
                >
            </li>
        </ul>
    {/if}
</header>
