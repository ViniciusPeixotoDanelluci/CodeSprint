<script lang="ts">
	import { CodeXmlIcon, Undo2 } from '@lucide/svelte';
    import '../common.css'
	import { page } from '$app/state';

    
</script>

<header class="background-grid">
    <nav class="flex-row justify-between">
        <div class="flex-row">
            <div class="codesprint flex-row">
                <div class="xml-icon flex-col">
                    <CodeXmlIcon size={"2rem"} strokeWidth={2.75} />
                </div>
                <div class="flex-col">
                    <div class="title">
                        Code Sprint
                    </div>
                    <div class="subtitle">
                        Beta Version / 2026
                    </div>
                </div>
            </div>
            <div class="task-title flex-row align-center">
                <div>
                    Maratona
                </div>
                {#if page.url.pathname !== ("/dashboard")}
                    <div>&nbsp;&nbsp;/&nbsp;&nbsp;</div>
                    <div>
                        Questão 01
                    </div>
                {/if}
            </div>
        </div>
        <div class="nav-right flex-col justify-center">
            <button class="return flex-row align-center justify-between">
                <Undo2 size={20}/>
                <div>
                    Voltar
                </div>
            </button>
        </div>
    </nav>
</header>

<style>
    /* ou .topbar */
    header {
        font-family: 'IBM Plex Mono';
        padding: 1.15rem;
        background-color: #fffef9;
        border-bottom: 2px solid #a2a78c;
    }

    .codesprint { 
        position: relative;
        width: 14rem; 
        border-right: 2px solid #a2a78c;
    }
    
    .xml-icon {
        position: relative;
        background-color: rgb(115, 204, 255);
        border: rgb(70, 39, 0) solid 2px;
        padding: 0.35rem;
        margin-right: 0.85rem;
        transform: rotate(-3deg);
        box-shadow: 3.5px 3.5px 0 #f7ad53;
    }

    .title {
        font-size: var(--fs-500);
        font-weight: bold;
    }

    .subtitle {
        font-size: var(--fs-300);
        color: rgb(46, 44, 44);
    }

    .task-title {
        font-family: 'Space Grotesk';
        font-weight: normal;
        font-size: var(--fs-400);
        margin-left: 1rem;
        :last-child {
            font-weight: bold;
        }
    }

    .return {
        font-family: 'Geist Sans';
        height: 2.5rem;
        min-width: 5.5rem;
        padding-inline: 0.45rem;
        background-color: #f2f1fa;
        border: 2px solid #353633;
        border-radius: 0.15rem;
        &:hover {
            background-color: #d3b4ec;
        }
    }
</style>
