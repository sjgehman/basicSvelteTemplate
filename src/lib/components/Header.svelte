<script lang="ts">
    import Sun from "lucide-svelte/icons/sun";
    import Moon from "lucide-svelte/icons/moon";

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
    class="text-header-foreground border-b border-gray-400 dark:border-gray-700"
    style="background-color: hsl(var(--header-background));"
>
    <nav class="container mx-auto px-4 py-3 flex justify-between items-center">
        <!-- Desktop Menu -->
        <ul class="hidden md:flex space-x-6">
            <li><a href="/" class="hover:text-gray-300">Home</a></li>
            <li><a href="#" class="hover:text-gray-300">About</a></li>
            <li><a href="#" class="hover:text-gray-300">Contact</a></li>
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

        <!-- Right Icon -->
        <div class="relative">
            <DropdownMenu.Root>
                <DropdownMenu.Trigger
                    class={buttonVariants({ variant: "outline", size: "icon" })}
                >
                    <Sun
                        class="h-[1.2rem] w-[1.2rem] rotate-0 scale-100 transition-all dark:-rotate-90 dark:scale-0 text-header-foreground"
                    />
                    <Moon
                        class="absolute h-[1.2rem] w-[1.2rem] rotate-90 scale-0 transition-all dark:rotate-0 dark:scale-100 text-header-foreground"
                    />
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
                <a href="/" class="block px-4 py-2 hover:bg-muted hover:text-muted-foreground" on:click={closeMenu}
                    >Home</a
                >
            </li>
            <li>
                <a href="#" class="block px-4 py-2 hover:bg-muted hover:text-muted-foreground" on:click={closeMenu}
                    >About</a
                >
            </li>
            <li>
                <a href="#" class="block px-4 py-2 hover:bg-muted hover:text-muted-foreground" on:click={closeMenu}
                    >Contact</a
                >
            </li>
        </ul>
    {/if}
</header>
