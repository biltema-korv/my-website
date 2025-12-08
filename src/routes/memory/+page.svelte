<script>
    let cards=$state([0,1,2,3,4,5,6,7,8,9,10,11])
    let bluePoints=0
    let redPoints=0
    let blueTurn=true

    let frontimage = "https://upload.wikimedia.org/wikipedia/commons/6/68/Joe_Biden_presidential_portrait.jpg"
    let backimage = "https://upload.wikimedia.org/wikipedia/commons/thumb/8/8d/President_Barack_Obama.jpg/961px-President_Barack_Obama.jpg"
</script>  

<main>
    <h1 class="rubrik">Memory</h1>

    
    <div class="memory">
        {#each cards as card}
            <div class="card">
                <img class="front" src={frontimage} alt="Kortlek framsida">
                <img class="back" src={backimage} alt="Kortlek baksida">
            </div>
        {/each}
    </div>
</main>

<aside class="red">
    <p>{redPoints}</p>
</aside>

<aside class="blue">
    <p>{bluePoints}</p>
</aside>

<aside class="turn">
    class:blue= { blueTurn }
</aside>


<style>
    .rubrik{
        font-size: 50px;
        text-align: center;
    }

    .memory{
        grid-template-columns: repeat(4, 100px);
        grid-template-rows: repeat(3, 100px);
        display: grid;
        gap: 10px;
        justify-content: center;
    }

    .card{
        border-radius: 15px;
        width: 100%;
        height: 100%;
        background-color: white;
        border: 1px solid black;
        box-shadow: 4px 8px 10px rgba(0,0,0,0.2);
        position: relative;
    }

    .front{
        width:100%;
        height:100%;
        position:absolute;
        z-index: 2;
        border-radius: 15px;
    }

    .back{
        width:100%;
        height:100%;
        position:absolute;
        border-radius: 15px;
    }

    .red{
        width: 100px;
        height: 100px;
        position: fixed;
        bottom: 10px;
        right: 10px;
        background-color: red;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .blue{
        width: 100px;
        height: 100px;
        position: fixed;
        bottom: 10px;
        left: 10px;
        background-color: lightblue;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .turn{
        box-shadow: 0 0 10px 10px yellowgreen;
        z-index: -1;
    }

    p{
        font-size: 30px;
    }
</style>