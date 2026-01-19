<script>
    let frontimage = "https://www.sitesmartehandel.se/static/files/8/banan.jpg"
    let backimage0 = "https://upload.wikimedia.org/wikipedia/commons/thumb/8/8d/President_Barack_Obama.jpg/961px-President_Barack_Obama.jpg"
    let backimage1 = "https://upload.wikimedia.org/wikipedia/commons/thumb/e/e9/Official_portrait_of_Barack_Obama.jpg/250px-Official_portrait_of_Barack_Obama.jpg"
    let backimage2 = "https://prodbfopusgeneral.blob.core.windows.net/asset-storage-public/forfattarfotonstandard/g/24371g.jpg?timestamp=20240516062643"
    let backimage3 = "https://media.gq.com/photos/56436afea3bd50211a99c42d/master/w_1600%2Cc_limit/obama-gq-1215-05.jpg"
    let backimage4 = "https://preview.redd.it/former-president-barack-obama-at-age-63-v0-ghc7v0ur86se1.jpeg?auto=webp&s=7151d3a78b66cb5e85bccb30b3f55d38068db12a"
    let backimage5 = "https://cdn.britannica.com/19/101219-050-A07A26EF/Barack-Obama.jpg"

    let backimages = [
        backimage0, backimage0,
        backimage1, backimage1,
        backimage2, backimage2,
        backimage3, backimage3,
        backimage4, backimage4,
        backimage5, backimage5
    ];

    backimages = backimages
        .map(v => ({ val: v, key: Math.random() }))
        .sort((a, b) => a.key - b.key)
        .map(o => o.val);

    let cards = $state(
        backimages.map((img, n) => ({
            id: n,
            flipped: false,
            matched: false,
            image: img
        }))
    );

    let flipcount = 0;
    let bluePoints = $state(0);
    let redPoints = $state(0);
    let blueTurn = $state(true);
    let gameOver = $state(false);

    function restart() {
        bluePoints = 0;
        redPoints = 0;
        blueTurn = true;
        gameOver = false;
        flipcount = 0;

        backimages = [
            backimage0, backimage0,
            backimage1, backimage1,
            backimage2, backimage2,
            backimage3, backimage3,
            backimage4, backimage4,
            backimage5, backimage5
        ];

        backimages = backimages
            .map(v => ({ val: v, key: Math.random() }))
            .sort((a, b) => a.key - b.key)
            .map(o => o.val);

        cards = (
            backimages.map((img, n) => ({
                id: n,
                flipped: false,
                matched: false,
                image: img
            }))
        );
    }

    function flip(thecard) {
        if (thecard.flipped === true || gameOver) {
            return;
        }

        flipcount += 1;
        if (flipcount > 2) {
            return;
        }
        thecard.flipped = true;

        if (flipcount === 2) {
            setTimeout(() => {
                const cardflips = cards.filter(c => c.flipped && !c.matched);

                if (cardflips.length !== 2) {
                    flipcount = 0;
                    return;
                }

                const matchig = cardflips[0].image === cardflips[1].image;

                cardflips.forEach(c => {
                    if (matchig) {
                        c.matched = true;
                        if (blueTurn === true) {
                            bluePoints += 0.5;
                        } else {
                            redPoints += 0.5;
                        }
                    } else {
                        c.flipped = false;
                    }
                });

                blueTurn = !blueTurn;
                flipcount = 0;

                if (cards.every(c => c.matched)) {
                    gameOver = true;
                }

                cards = cards;
            }, 1000);
        }
    }
</script>

<main>
    <h1 class="rubrik">Memory</h1>
    <div class="memory">
        {#each cards as card}
            <button class="card" class:flipped={card.flipped} onclick={() => flip(card)}>
                <img class="front" src={frontimage} alt="Kortlek framsida">
                <img class="back" src={card.image} alt="Kortlek baksida">
            </button>
        {/each}
    </div>
</main>

<aside>
    <p>{redPoints}</p>
</aside>

<aside class="blue">
    <p>{bluePoints}</p>
</aside>

<aside class="turn" class:blue={blueTurn}></aside>

<button onclick={() => restart()} aria-label="Restart game">
    <p>Restart</p>
</button>

{#if gameOver}
    <div class="game-over">
        <p>Game Over</p>
        <p>
            {#if bluePoints > redPoints}
                Player 1 (Blue) Wins
            {:else if redPoints > bluePoints}
                Player 2 (Red) Wins
            {:else}
                Tie
            {/if}
        </p>
    </div>
{/if}

<style>
    .rubrik {
        font-size: 50px;
        text-align: center;
    }

    .memory {
        grid-template-columns: repeat(4, 100px);
        grid-template-rows: repeat(3, 100px);
        display: grid;
        position: relative;
        gap: 10px;
        justify-content: center;
    }

    .card {
        border-radius: 15px;
        width: 100%;
        height: 100%;
        background-color: white;
        border: 1px solid black;
        box-shadow: 4px 8px 10px rgba(0, 0, 0, 0.2);
        position: relative;
        backface-visibility: hidden;
        transform-style: preserve-3d;
        transition: transform 0.5s;
    }

    .front {
        width: 100%;
        height: 100%;
        position: absolute;
        top: 0;
        left: 0;
        z-index: 2;
        border-radius: 14px;
    }

    .back {
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        position: absolute;
        border-radius: 14px;
        transform: rotateY(180deg);
    }

    aside {
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

    button {
        width: 200px;
        height: 100px;
        position: fixed;
        bottom: 10px;
        left: 0;
        right: 0;
        margin-left: auto;
        margin-right: auto;
        background-color: gray;
        display: flex;
        justify-content: center;
        align-items: center;
    }


    .blue {
        left: 10px;
        background-color: blue;
    }

    .flipped {
        transform: rotateY(180deg);
    }

    .turn {
        box-shadow: 0 0 10px 10px yellowgreen;
        z-index: -1;
    }

    .game-over {
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: white;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 0 15px rgba(0, 0, 0, 0.3);
    }

    p {
        font-size: 30px;
    }

    .card:not(.flipped):hover {
        transform: scale(1.1);
    }


    @media (min-height: 500px){
        .memory{
            grid-template-columns: repeat(4, 100px);
            grid-template-rows: repeat(3, 100px);
        }
    }
    @media (max-height: 500px){
        .memory{
            grid-template-columns: repeat(6, 100px);
            grid-template-rows: repeat(2, 100px);
        }
    }
</style>
