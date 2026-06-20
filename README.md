# U.I.T-VERIFICATION-
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Vérification U.I.T</title>

<style>
body{
    font-family: Arial, sans-serif;
    background:#111;
    color:white;
    text-align:center;
    padding:50px;
}

.container{
    max-width:600px;
    margin:auto;
    background:#1c1c1c;
    padding:30px;
    border-radius:15px;
}

input{
    width:80%;
    padding:12px;
    margin:15px 0;
    border:none;
    border-radius:8px;
}

button{
    padding:12px 25px;
    border:none;
    border-radius:8px;
    cursor:pointer;
    background:gold;
    font-weight:bold;
}

#result{
    margin-top:25px;
    font-size:22px;
}
</style>
</head>

<body>

<div class="container">

<h1>U.I.T</h1>
<h2>Unité d'Instruction Tactique</h2>

<p>Vérification de fin de formation</p>

<input type="text" id="matricule"
placeholder="Ex : UIT-2026-001">

<br>

<button onclick="verifier()">
Vérifier
</button>

<div id="result"></div>

</div>

<script>

const soldatsValides = {
"UIT-2026-001":{
nom:"John Walker",
grade:"Soldat",
promotion:"Alpha 2026"
},

"UIT-2026-002":{
nom:"Mike Brown",
grade:"Caporal",
promotion:"Bravo 2026"
}
};

function verifier(){

let matricule =
document.getElementById("matricule")
.value.toUpperCase();

let result =
document.getElementById("result");

if(soldatsValides[matricule]){

let s = soldatsValides[matricule];

result.innerHTML = `
<div style="color:lime">
✅ FORMATION VALIDÉE
</div>

<br>

Nom : ${s.nom}<br>
Grade : ${s.grade}<br>
Promotion : ${s.promotion}<br><br>

Lead : Ange Kassano<br>
Co-Lead : MR Ritchy
`;

}else{

result.innerHTML = `
<div style="color:red">
❌ FORMATION NON VALIDÉE
</div>
`;
}

}
</script>

</body>
</html>
