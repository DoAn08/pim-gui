<script lang="ts">
    let files:any;
    let useYouTube:boolean = true;
    function changeMode() {
        useYouTube = !useYouTube;
    }
</script>

<style lang="scss">
button {
    border: none;
    background-color: rgba(51, 51, 51, 0);
    color: var(--cmp);
    height: 48px; width: 48px;
}
button:hover {
    transition: all 0.1s ease-out;
    background-color: var(--cmp);
    color: var(--bg);
}
p {
    margin: 0;
}
.bar {
    display: flex;
    width: calc(100vw - 48px);
    .searchInput {
        height: 48px;
        line-height: 48px;
        font-size: 16px;
        background-color: inherit;
        border: none;
        font-family: "Roboto Mono", monospace;
        width: 100%;
        margin-inline-start: 12px;
        color: var(--cmp);
    }
    .searchInput:focus {
        outline: none;
    }
    .searchInput:focus::placeholder {
        color: #888888;
    }
    .searchInput::-webkit-search-cancel-button {
        display: none;
    }
    .fileInput {
        width: 48px;
        height: 48px;
        input {
            display: none;
        }
    }
    .fileName {
        width: calc(100vw - 96px);
        height: 48px;
        line-height: 48px;
        margin-inline-start: 12px;
    }
}
</style>

<div class="queueControl">
    <div class="searchBarWrapper" >
        <form action="" class="bar"> <!--process search-->
            {#if useYouTube}
            <input type="url" placeholder="Input YouTube video / playlist link..." class="searchInput" name="s" autocomplete="off">
            <button type="submit"><span class="material-symbols-rounded">add</span></button>
            <button on:click={changeMode}><span class="material-symbols-rounded">change_circle</span></button>
            {:else} 
            <button class="material-symbols-rounded" on:click={() => {
                document.getElementById("filei").click();
            }}>
                <label class="fileInput">
                    <span>upload</span>
                    <input type="file" accept="audio/*" id="filei" bind:files />
                </label>
            </button>
            <p class="fileName">{#if files}{files[0].name}{:else}⠀{/if}</p>
            <button type="submit"><span class="material-symbols-rounded">add</span></button>
            <button on:click={changeMode}><span class="material-symbols-rounded">change_circle</span></button>
            {/if}
        </form>
    </div>
</div>
