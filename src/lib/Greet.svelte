<script lang="ts">
    import { invoke } from "@tauri-apps/api/tauri";

    let name = "";
    let greetMsg = "";

    async function greet() {
        // Learn more about Tauri commands at https://tauri.app/v1/guides/features/command
        greetMsg = await invoke("greet", { name });
    }

    async function executeCommands() {
        const message = await invoke("command_with_message", {
            message: "some mesage",
        });
        console.log(message);
    }
</script>

<div>
    <form class="row" on:submit|preventDefault={greet}>
        <input
            id="greet-input"
            placeholder="Enter a name..."
            bind:value={name}
        />
        <button type="submit">Greet</button>
    </form>
    <button on:click={executeCommands}>Click to execute command</button>
    <p>{greetMsg}</p>
</div>
