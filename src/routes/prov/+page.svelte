<script>
    let amount=[0,1,2,3,4,5]
</script>

<main>
    <div class="main">
        <div class="yellow">1</div>
        <div class="green">2</div>
        <div class="red">3</div>
        <div class="purple">4</div>
        <div class="orange">5</div>
        <div class="grid">6</div>
    </div>
</main>

<style>
    .main{
        grid-template-columns: repeat(3, 1fr);
        grid-template-rows: repeat(2, 1fr);
        align-items: center;
        flex-direction: row;
        display:grid;
        width: 440px;
        height: 240px;
        background: gray;
    }
    .grid{
        width:50px;
        height:20px;
        align-items:center;
        padding: 40px;
        margin: 10px;
        background: blue;
        border-radius: 15px;
        text-align:center;
        color: white;
    }
    .red{
        width:50px;
        height:20px;
        align-items:center;
        padding: 40px;
        margin: 10px;
        background: red;
        border-radius: 15px;
        text-align:center;
        color: white;
    }
    .green{
        width:50px;
        height:20px;
        align-items:center;
        padding: 40px;
        margin: 10px;
        background: green;
        border-radius: 15px;
        text-align:center;
        color: white;

    }
    .yellow{
        width:50px;
        height:20px;
        align-items:center;
        padding: 40px;
        margin: 10px;
        background: yellow;
        border-radius: 15px;
        text-align:center;
        color: white;

    }
    .purple{
        width:50px;
        height:20px;
        align-items:center;
        padding: 40px;
        margin: 10px;
        background: purple;
        border-radius: 15px;
        text-align:center;
        color: white;

    }
    .orange{
        width:50px;
        height:20px;
        align-items:center;
        padding: 40px;
        margin: 10px;
        background: orange;
        border-radius: 15px;
        text-align:center;
        color: white;

    }
</style>