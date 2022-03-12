<script>
    import {onMount} from "svelte";
    import {t} from '$lib/translations'
    import {ClassColorScheme, ColorSchemeStore} from "$lib/shares/js/ClassColorScheme/ClassColorScheme"

    let colorScheme,
        valColorScheme
    export let mode,
        className

    ColorSchemeStore.colorScheme.subscribe((obj) => {
        valColorScheme = obj
    })

    const switcherColorScheme = () => {
        colorScheme.switch()
    }

    onMount(async () => {
        colorScheme = new ClassColorScheme()
    })
</script>

<span class="curPoi notSel" title={$t(`common.valColorScheme.${valColorScheme}`)} on:click={switcherColorScheme}>
    {#if mode === 'string'}
        <a href={"javascript:void(0)"} class={className}>
            {$t(`common.colorScheme.${valColorScheme}To`)}
        </a>
    {:else}
        <i class="fa-solid fa-circle-half-stroke"></i>
    {/if}
</span>
