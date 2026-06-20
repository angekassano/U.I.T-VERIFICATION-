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
placeholder="Ex :entrer le nom">

<br>

<button onclick="verifier()">
Vérifier
</button>

<div id="result"></div>

</div>

<script>

<script>
const soldatsValides = {
    "Kassano Ange": {
        nom: "Kassano Ange",
        grade: "Soldat",
        promotion: "2026"
    },
    "Mr Ritchy": {
        nom: "Mr Ritchy",
        grade: "Caporal",
        promotion: "2026"
    }
    
};

function verifier() {
    const input = document.getElementById("nom").value.trim();  
    const resultDiv = document.getElementById("result");

    
    resultDiv.innerHTML = "";

    if (!input) {
        resultDiv.innerHTML = `<p style="color: orange;">⚠️ Veuillez entrer un nom</p>`;
        return;
    }

    const soldat = soldatsValides[input];

    if (soldat) {
        resultDiv.innerHTML = `
            <p style="color: green; font-weight: bold;">
                ✅ Valide - Formation terminée<br><br>
                Nom : ${soldat.nom}<br>
                Grade : ${soldat.grade}<br>
                Promotion : ${soldat.promotion}
            </p>`;
    } else {
        resultDiv.innerHTML = `
            <p style="color: red; font-weight: bold;">
                ❌ Non trouvé<br><br>
                Le nom <strong>"${input}"</strong> n'a pas fait la formation ou n'existe pas dans la liste.
            </p>`;
    }
}
</script>

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
