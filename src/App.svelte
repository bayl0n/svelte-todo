<script>
    import { fade, fly } from 'svelte/transition';
    let todos = [
        { done:false, text: 'eat' },
        { done:false, text: 'sleep' },
        { done:false, text: 'code' },
        { done:false, text: 'repeat' }
    ];

    function toggleDone(t) {
        todos = todos.map(todo => {
            if(todo === t) return { done: !t.done, text: t.text };
            return todo;
        });
    }

    let hideDone = false;

    $:showing = filtered.length

    $:filtered = hideDone
        ? todos.filter(todo => !todo.done)
        : todos;
</script>

<label>
    <input
    type="checkbox"
    bind:checked={hideDone}
    >
    
    hide done
</label>

<p>showing {showing} of {todos.length}</p>

<ul>
    {#each filtered as todo}
    <li on:click={toggleDone(todo)} in:fade>
        {todo.done ? '👍' : ''} {todo.text}
    </li>
    {/each}
</ul>