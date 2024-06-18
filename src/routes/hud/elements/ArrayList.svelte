<script lang="ts">
    import {onMount} from "svelte";
    import type {Module} from "../../../integration/types";
    import {getModules} from "../../../integration/rest";
    import {listen} from "../../../integration/ws";
    import {getTextWidth} from "../../../integration/text_measurement";
    import {flip} from "svelte/animate";
    import {fly} from "svelte/transition";
    import {convertToSpacedString, spaceSeperatedNames} from "../../../theme/theme_config";

    let enabledModules: Module[] = [];

    async function updateEnabledModules() {
        enabledModules = (await getModules())
            .filter((m) => m.enabled && !m.hidden)
            .sort(
                (a, b) =>
                    getTextWidth($spaceSeperatedNames ? convertToSpacedString(b.name) : b.name, "500 14px Inter") -
                    getTextWidth($spaceSeperatedNames ? convertToSpacedString(a.name) : a.name, "500 14px Inter"),
            );
    }

    spaceSeperatedNames.subscribe(async () => {
        await updateEnabledModules();
    });

    onMount(async () => {
        await updateEnabledModules();
    });

    listen("toggleModule", async () => {
        await updateEnabledModules();
    });

    listen("refreshArrayList", async () => {
        await updateEnabledModules();
    });
</script>

<div class="arraylist">
    {#each enabledModules as { name } (name)}
        <div class="module" animate:flip={{ duration: 200 }} in:fly={{ x: 50, duration: 200 }}>
            {$spaceSeperatedNames ? convertToSpacedString(name) : name}
        </div>
    {/each}
</div>

<style lang="scss">
    @import "../../../colors.scss";

    .arraylist {
        //position: fixed;
        //top: 0;
        //right: 0;
    }

    .module {
        //background-color: rgba($arraylist-base-color, 0.05);
        color: $arraylist-text-color;
        //color: black;
        font-size: 20px;
        //border-radius: 10px;
        padding: 5px 8px;
        //border-left: solid 4px $accent-color;
        width: max-content;
        //margin-bottom: 10px;
        font-weight: 100;
        margin-left: auto;
        //box-shadow: 0px 0px 5px 5px rgba(black, 0.5), inset 0px 0px 10px rgba(black, 0.5);
        //text-shadow: 0px 0px 20px rgba(black, 1);
    }
</style>
