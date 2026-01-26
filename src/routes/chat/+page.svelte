<script>
    import ElizaBot from 'elizabot'; 
    import { enhance } from "$app/forms";
    const eliza = new ElizaBot();
    let chat = $state([{ user: 'Eliza', message: eliza.getInitial() }]);

    
    function write(text) {
        if (!text) return;

        chat = [
            ...chat,
            { user: 'User', message: text },
            { user: 'Eliza', message: eliza.transform(text) }
        ];
    }
</script>

<main>
    <section>
        {#each chat as msg}
            <article>
                <p>{msg.message}</p>
            </article>
        {/each}
    </section>  
    
    <form  method="post"
        use:enhance={({ formElement, formData, action, cancel }) => {
        cancel(); //don't post anything to server
        const text = formData.get("text"); // what does "text" refer to?
        write(text);

        // TODO: reset the form using _____.reset() - what do we want to reset? the element or the data?

        formData.reset()

        }}>
                
        <input type="text" name="text" placeholder="Skriv ett meddelande">
    </form>
</main>

<style>
    main {
        width: 60vw;
        height: 70vh;
        padding: 10px;
        background-color: royalblue;
        margin: auto;
        display: grid;
        grid-template-rows: 90% 10%;
        border-radius: 25px;
    }

    section {
        overflow-y:scroll
    }

    article {
        margin: 10px;
        padding: 10px;
        border-radius: 10px;
        width: 90%;
        background-color: dodgerblue;
    } 


    input {
        width: 90%;
        height: 60%;
        margin: auto;
        background-color: dodgerblue;
        border: 3px solid cornflowerblue;
        border-radius: 15px;
    }
</style>
