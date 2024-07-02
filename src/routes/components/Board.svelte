<script lang="ts">
    let currentPlayer: string = "X";
    let items = [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""],
    ];
    const win = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
    ];

    let player: string = "X";

    let options: Array<string> = ["", "", "", "", "", "", "", "", ""];

    function boxClick(x: number, y: number) {
        const index = y + x * 3;
        if (options[index] != "") {
            return;
        }
        updateBox(index, x, y);
        checkWinner();
    }

    function updateBox(index: number, x: number, y: number) {
        options[index] = player;
        items[x][y] = currentPlayer;
    }

    function changePlayer() {
        player = player == "X" ? "O" : "X";
        currentPlayer = currentPlayer == "X" ? "O" : "X";
    }

    function checkWinner() {
        let isWon = false;
        for (let i = 0; i < win.length; i++) {
            const condition = win[i]; //[0,1,2]
            const box1 = options[condition[0]]; //x
            const box2 = options[condition[1]]; //''
            const box3 = options[condition[2]]; //''
            if (box1 == "" || box2 == "" || box3 == "") {
                continue;
            }
            if (box1 == box2 && box2 == box3) {
                isWon = true;
                alert(currentPlayer + " Wined");
                restartGame();
            }
        }

        if (!isWon || options.includes("")) {
            changePlayer();
        }
    }

    function restartGame() {
        options = ["", "", "", "", "", "", "", "", ""];
        currentPlayer = "X";
        player = "X";
        items = [
            ["", "", ""],
            ["", "", ""],
            ["", "", ""],
        ];
    }
</script>

<div class="board">
    {#each items as board, x}
        {#each board as item, y}
            <div class="item" on:click={() => boxClick(x, y)}>{item}</div>
        {/each}
    {/each}
</div>

<button class="reset-game" on:click={restartGame}>Reset Game</button>

<style>
    * {
        box-sizing: border-box;
    }
    .board {
        width: 300px;
        display: flex;
        align-items: flex-start;
        margin: 20px auto;
        flex-wrap: wrap;
    }
    .board .item {
        width: 100px;
        height: 100px;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 25px;
        border: 2px solid #eccc68;
        cursor: pointer;
    }
    button {
        width: 150px;
        height: 40px;
        font-size: 18px;
        color: white;
        background-color: #ff4757;
        border: none;
        border-radius: 3px;
        margin: 10px auto;
    }
</style>
