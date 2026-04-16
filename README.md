<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Currency Exchange</title>

<style>
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: #f2f2f2;
}

.header {
    background: #120a5c;
    color: white;
    text-align: center;
    padding: 40px 0;
}

.container {
    display: flex;
    justify-content: center;
    margin-top: -40px;
}

.card {
    background: white;
    padding: 30px;
    width: 600px;
    box-shadow: 0 2px 6px rgba(0,0,0,0.2);
}

.row {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
}

.field {
    display: flex;
    flex-direction: column;
    width: 30%;
}

label {
    font-size: 12px;
    margin-bottom: 5px;
}

input, select {
    padding: 8px;
    border: 1px solid #ccc;
}

button {
    background: #120a5c;
    color: white;
    border: none;
    padding: 10px 30px;
    cursor: pointer;
}

.result strong {
    display: block;
    font-size: 22px;
    margin-top: 5px;
}
</style>
</head>

<body>

<div class="header">
    <h1>XYZ-COMPANY</h1>
    <p>CURRENCY EXCHANGE PLATFORM</p>
</div>

<div class="container">
<div class="card">

    <div class="row">
        <div class="field">
            <label>Amount</label>
            <input type="number" id="amount" value="100">
        </div>

        <div class="field">
            <label>From</label>
            <select id="from">
                <option value="USD">USD - $</option>
                <option value="EUR">EUR - €</option>
                <option value="EGP">Pound - £</option>
                <option value="RWF">RWF</option>
            </select>
        </div>

        <div class="field">
            <label>To</label>
            <select id="to">
                <option value="RWF">RWF</option>
                <option value="USD">USD - $</option>
                <option value="EUR">EUR - €</option>
                <option value="EGP">Pound - £</option>
            </select>
        </div>
    </div>

    <div class="row">
        <button onclick="convert()">Convert</button>

        <div class="result">
            Result
            <strong id="result">---</strong>
        </div>
    </div>

</div>
</div>

<script>
async function convert() {
    let amount = document.getElementById("amount").value;
    let from = document.getElementById("from").value;
    let to = document.getElementById("to").value;

    if (amount === "" || amount <= 0) {
        alert("Enter valid amount");
        return;
    }

    try {
        let res = await fetch(`https://api.exchangerate-api.com/v4/latest/${from}`);
        let data = await res.json();

        let rate = data.rates[to];
        let result = amount * rate;

        document.getElementById("result").innerText = result.toLocaleString();
    } catch (error) {
        document.getElementById("result").innerText = "Error";
    }
}
</script>

</body>
</html>
