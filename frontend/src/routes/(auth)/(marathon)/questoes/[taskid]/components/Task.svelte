<script lang="ts">
	// @ts-expect-error
    import MockMarkdown from '#lib/data/mock_markdown.md'
</script>

<MockMarkdown />

<style>
    :global(h1) {
        margin: 0;
    }
    :global(pre) {
        white-space: pre-wrap;
        overflow-wrap: anywhere;
    }
</style>