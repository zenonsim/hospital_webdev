<template>
    <div id = "container"></div>
        <form id = "myform">
            <h2>Add Coins </h2>
            
            <div class = "formli">
                <label for="coin1"> Coin Name: </label>
                <input type="text" id="coin1" required="" placeholder = "Enter Coin"> <br><br>
                <label for="ticker1"> Ticker: </label>
                <input type="text" id="ticker1" required="" placeholder = "Valid Ticker"> <br><br>
                <label for="buy1"> Buy Price: </label>
                <input type="number" id="buy1" required="" placeholder = "Buy Price"> <br><br>
                <label for="quant1"> Buy Quantity: </label>
                <input type="number" id="quant1" required="" placeholder = "Quantity"> <br><br>

                <div class = "save">
                    <button id = "savebutton" type = "button" v-on:click = "savetofs()"> Save </button>
                </div>
            </div>
        </form>

</template>

<script>
import firebaseApp from '../firebase.js';
import { getFirestore } from "firebase/firestore";
import {doc, setDoc} from "firebase/firestore"
const db = getFirestore(firebaseApp);

export default {

    methods: {
        async savetofs(){
        var a = document.getElementById("coin1").value;
        var b = document.getElementById("ticker1").value;
        var c = document.getElementById("buy1").value;
        var d = document.getElementById("quant1").value;
        console.log(a)
        console.log(b)
        console.log(c)
        console.log(d)
        alert("Saving your data for coin: " + a)

        try{
            const docRef = await setDoc(doc(db, "Portfolio", a), {Coin: a, Ticker: b, Buy_Price: c, Buy_Quantity: d})
            console.log(docRef)
            document.getElementById('myform').reset();
            this.$emit("added")

        } catch (error) {
            console.error("Error adding document: ", error)
        }

        }
    }
}
</script>

<style scoped>

    h2{
        background-color:yellow;
    }

    .formli{
        display: inline-block;
        text-align: right;
    }

    form{
        text-align: center;
        align-items: center;
        margin: auto;
    }

    input:hover {
        box-shadow: 3px 3px purple;
        border-radius: 2px;
    }

    .save{
        text-align: center;
    }

</style>