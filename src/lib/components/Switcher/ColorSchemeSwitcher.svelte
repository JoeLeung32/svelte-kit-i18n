<script>
    import {onMount} from "svelte";
    import {t} from '$lib/translations'
    import {ClassColorScheme, colorScheme} from "$lib/shares/js/ClassColorScheme/ClassColorScheme"

    let colorSchemeController
    export let mode

    const switcherColorScheme = () => {
        colorSchemeController.switch()
    }

    onMount(async () => {
        colorSchemeController = new ClassColorScheme()
    })
</script>

<span class="curPoi notSel" title={$t(`common.colorScheme.${$colorScheme}`)} on:click={switcherColorScheme}>
    {#if mode === 'string'}
        <a href={"javascript:void(0)"}>
            {$t(`common.colorScheme.${$colorScheme}To`)}
        </a>
    {:else}
        <i class="fa-solid fa-circle-half-stroke"></i>
    {/if}
</span>
