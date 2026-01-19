
<script>
    import { fade } from 'svelte/transition'
    let varor=$state([{ name:"Mjölk", purchased: false, priority: 0}]);
    let tobuy=$state("")
    let priority=$state("")

    function handleSubmit(which){
        if(which.length === 0){
            return;
        }

        varor.push({
            name: which,
            purchased: false,
            priority: 0
        });
    }

    function prioritisation(priorities,which){
        if(priority.length === 0){
            return;
        }

        which.priority=priorities
        console.log(which.priority)
    }

    function remove(which){
        const index = varor.indexOf(which);

        if (index !== -1) {
            varor.splice(index, 1); 
        }
    }
    
    function purchased(which){
        which.purchased=!which.purchased
    }
</script>


<main class="container">

    <h1>Shoppinglist</h1>
    <div class="categories_container">
        <section>
            <h2>Varor att köpa</h2>
                <div class="empty">
                    <ul>
                        {#each varor.filter(v => !v.purchased).sort((a, b) => b.priority - a.priority) as vara}
                            <li transition:fade>
                                { vara.name }
                                <button onclick={() => remove(vara)}>🗑️</button>
                                <button onclick={() => purchased(vara)}>➡️</button>

                                <input type="number" bind:value={vara.priority}>
                            </li>
                        {/each }
                    </ul>
                </div>
                <label for="Purchased">Lägg till varor att köpa:</label>
            <input type="text" bind:value ={tobuy}>
            <br>

            <button onclick={() => handleSubmit(tobuy)}>Sätt i listan</button>
        </section>
        
        <section>
            <h2>Köpta varor</h2>
                <div class="mt">
                    <ul>
                        {#each varor.filter(v => v.purchased).sort((a, b) => b.priority - a.priority) as vara}
                            <li transition:fade>
                                { vara.name }
                                <button onclick={() => remove(vara)}>🗑️</button>
                                <button onclick={() => purchased(vara)}>⬅️</button>
                                <input type="number" bind:value={vara.priority}>
                            </li>
                        {/each }
                    </ul> 
                </div>
        </section>
    </div>
</main>

<style>
    li{
        list-style-position:inside;
        border-bottom: 1px solid white;
        padding: 0.5rem;
        border-radius: 5px;
    }
    .container{
        background-color: #4a412a;
        width: 60vw;
        height: 55vh;
        border-radius: 20px;
        display: flex;
        flex-direction: column;
        grid-template-rows: 1fr;
        margin: auto;
        padding: 20px 0;
    }

    input[type="number"]{
        width: 60px;
        background-color: #4a412a;
        color: white;
        border: 1x;
        border-radius: 50px;
    }

    .container > h1{
        background-color: #9aae07;
        grid-template-rows: 8fr;
        text-align: center;
        margin: 0;
    }

    button{
        background-color: #4a412a;
        color: white;
        border: 1x;
        border-radius: 100px;
    }

    .categories_container{
        background-color: #9aae07;
        width: 100%;
        display:flex;
        height: 50vh;
    }

    .empty{
        background-color: rgba(0, 0, 0, 0.1); /* svart bakgrund med 10% opacitet */
        width: 100%;
        display:flex;
        height: 33vh;
        text-align: left;
        overflow-y: auto;
    }

    .mt{
        background-color: rgba(0, 0, 0, 0.1); /* svart bakgrund med 10% opacitet */
        width: 100%;
        display:flex;
        height: 40vh;
        text-align: left;
        overflow-y: auto;
    }

    .categories_container section:first-child{  /* vilket barn vill vi styla? */
        background-color: rgba(0, 0, 0, 0.1); /* svart bakgrund med 10% opacitet */
        text-align: center;
        font-size: 20px;
        width: 50%;
        flex: 1;
        overflow-y: auto;
    }
 
    .categories_container section:nth-child(2){  /* vilket barn vill vi styla? */
        background-color: rgba(0, 0, 0, 0.2); /* svart bakgrund med 30% opacitet */
        text-align: center;
        font-size: 20px;
        width: 50%;
        flex: 1;
        overflow-y: auto;
    }
</style>