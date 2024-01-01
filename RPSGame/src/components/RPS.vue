<script>
export default{
    data(){
        return {
            likes: 0,
            UserChoice: "None",
            ComputerChoice: "None",
            Winner: "None",
            UserWins: localStorage.getItem("Wins"),
            ComputerWins: localStorage.getItem("Loses"),
            DisplayUserWins: localStorage.getItem("Wins"),
            DisplayComputerWins: localStorage.getItem("Loses"),
            StartGameDisplayStyle: false,
        }
    },
    methods: {
        StartGame(){
            this.StartGameDisplayStyle = true;
        },
        UserInput(value){
            let ComputerNoChoice;
            localStorage.setItem('Wins', this.UserWins);
            localStorage.setItem('Loses', this.ComputerWins);
            this.DisplayUserWins = localStorage.getItem('Wins');
            this.DisplayComputerWins = localStorage.getItem('Loses');
            if(value == 'R'){
                this.UserChoice = "Rock";
                ComputerNoChoice = Math.round(Math.random() * 3 + 1);
                switch (ComputerNoChoice) {
                    case 1:
                        this.Winner = "Tied";
                        this.ComputerChoice = "Rock";
                        break;
                    case 2:
                        this.Winner = "Computer";
                        this.ComputerWins++;
                        this.ComputerChoice = "Paper";
                        break;
                    case 3:
                        this.Winner = "User";
                        this.UserWins++;
                        this.ComputerChoice = "Scissors";
                        break;
                    default:
                        break;
                }
            }else if(value == 'P'){
                this.UserChoice = "Paper";
                ComputerNoChoice = Math.round(Math.random() * 3 + 1);
                switch (ComputerNoChoice) {
                    case 1:
                        this.ComputerChoice = "Rock";
                        this.UserWins++;
                        this.Winner = "User";
                        break;
                    case 2:
                        this.Winner = "Tied";
                        this.ComputerChoice = "Paper";
                        break;
                    case 3:
                        this.ComputerWins++;
                        this.ComputerChoice = "Scissors";
                        this.Winner = "Computer";
                        break;
                    default:
                        break;
                }
            }else if(value == 'S'){
                this.UserChoice = "Scissors";
                ComputerNoChoice = Math.round(Math.random() * 3 + 1);
                switch (ComputerNoChoice) {
                    case 1:
                        this.ComputerWins++;
                        this.Winner = "Computer";
                        this.ComputerChoice = "Rock";
                        break;
                    case 2:
                        this.Winner = "User";
                        this.UserWins++;
                        this.ComputerChoice = "Paper";
                        break;
                    case 3:
                        this.Winner = "Tied";
                        this.ComputerChoice = "Scissors";
                        break;
                    default:
                        break;
                }
            }else{
                console.log("User Selects Nothing")
            }
        },
        ResetScore(){
            this.UserWins = 0;
            this.ComputerWins = 0;
        }
    }
}
</script>
<template>
    <div class="firstLaunched" v-if="!StartGameDisplayStyle">
        <div class="startContainer">
            <h1>Want to Play Rock-Paper-Scissors?</h1>
            <button v-on:click="StartGame()">Play</button>
        </div>
    </div>
    <div class="header" v-if="StartGameDisplayStyle">
        <h1>Rock Paper Scissors</h1>
    </div>
    <div class="InGameContainer">
        <div class="InGame" v-if="StartGameDisplayStyle">
            <div class="InGameBtns">
                <button id="R" v-on:click="UserInput('R')"><img src="../assets/fist.png" alt="rockfist"></button>
                <button id="P" v-on:click="UserInput('P')"><img src="../assets/privacy.png" alt="handpaper"></button>
                <button id="S" v-on:click="UserInput('S')"><img src="../assets/scissors.png" alt="handscissor"></button>
            </div>
            <h2>User Selected: {{ UserChoice }} <br> Computer Selected: {{ ComputerChoice }}</h2>
            <h2>{{ Winner }} Wins!</h2>
            <h3>User: {{ DisplayUserWins }} wins <br> Computer: {{ DisplayComputerWins }} wins</h3>
            <button id="resetbtn" v-on:click="ResetScore()">Reset Score</button>
        </div>
    </div>
</template>