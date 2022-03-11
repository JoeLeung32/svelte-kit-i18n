<script>
    import {onMount} from "svelte";
    import Common from '$lib/stores/Common'
    import {t} from '$lib/translations'
    import {ClassColorScheme} from "$lib/shares/js/ClassColorScheme/ClassColorScheme"

    let colorScheme,
        valColorScheme

    Common.colorScheme.subscribe((obj) => {
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
    <i class="fa-solid fa-circle-half-stroke"></i>
</span>
