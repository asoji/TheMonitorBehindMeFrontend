<script lang="ts">

    let isVideo = false
    let media: string | null = null

    const client = new WebSocket("ws://127.0.0.1:12456")

    client.addEventListener("message", (message) => {
        let type
        let content

        try {
            const data = JSON.parse(message.data)
            type = data.type
            content = data.content
            console.log(data)
        } catch (e: any) {
            console.error(e)
            return
        }

        switch (type) {
            case "video/mp4":
            case "video/mpeg":
            case "video/x-msvideo":
            case "video/webm":
                isVideo = true
            default:
                isVideo = false
        }

        media = content
    })
</script>

{#if isVideo}
    <video src={media}></video>
{:else}
    <img src={media}>
{/if}

<svelte:head>
    <title>The Monitor Behind Me</title>
    <meta name="description" content="for people to troll me with the monitor behind me"/>
</svelte:head>

<style>

</style>
