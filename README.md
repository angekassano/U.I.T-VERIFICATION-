<!-- === SECTION VÉRIFICATION U.I.T === -->
<div style="background: #0a0a0a; border: 2px solid #4a4a4a; padding: 25px; max-width: 600px; margin: 20px auto; border-radius: 8px; box-shadow: 0 0 20px rgba(0, 255, 100, 0.1); font-family: 'Courier New', monospace;">
    
    <div style="text-align: center; margin-bottom: 20px;">
        <h2 style="color: #00ff80; margin: 0; letter-spacing: 3px; text-shadow: 0 0 10px #00ff80;">
            U.I.T — UNITÉ D'INTRUSION TACTIQUE
        </h2>
        <p style="color: #888; font-size: 14px; margin: 5px 0;">ARMÉE GLENDALE • VÉRIFICATION FORMATION</p>
    </div>

    <div style="margin-bottom: 15px;">
        <label style="color: #00ff80; font-size: 14px; display: block; margin-bottom: 5px;">NOM DU SOLDAT</label>
        <input type="text" id="nom" 
               placeholder="Ex: Kassano Ange" 
               style="width: 100%; padding: 12px; background: #111; border: 1px solid #00ff80; color: white; font-size: 16px; border-radius: 4px;">
    </div>

    <button onclick="verifier()" 
            style="width: 100%; padding: 14px; background: #00ff80; color: black; font-weight: bold; font-size: 16px; border: none; cursor: pointer; border-radius: 4px; letter-spacing: 2px;">
            VÉRIFIER ACCÈS
    </button>

    <div id="result" style="margin-top: 20px; min-height: 120px; padding: 15px; border-radius: 4px; font-size: 15px;"></div>
</div>

<script>
// Base de données des soldats validés
const soldatsValides = {
    "Kassano Ange": {
        nom: "Kassano Ange",
        grade: "Soldat",
        promotion: "2026",
        statut: "FORMATION TERMINÉE"
    },
    "Mr Ritchy": {
        nom: "Mr Ritchy",
        grade: "Caporal",
        promotion: "2026",
        statut: "FORMATION TERMINÉE"
    }
    "moubarak stone": {
        nom: "moubarak stone",
        grade: "rang3",
        promotion: "2026",
        statut: "FORMATION TERMINÉE"
};

function verifier() {
    const input = document.getElementById("nom").value.trim();
    const resultDiv = document.getElementById("result");

    resultDiv.innerHTML = "";

    if (!input) {
        resultDiv.innerHTML = `<p style="color: #ffaa00; text-align:center;">⚠️ VEuillez entrer un nom complet.</p>`;
        return;
    }

    const soldat = soldatsValides[input];

    if (soldat) {
        resultDiv.innerHTML = `
            <div style="background: rgba(0, 255, 100, 0.1); border: 1px solid #00ff80; padding: 15px; border-radius: 4px; text-align: center;">
                <h3 style="color: #00ff80; margin: 0 0 10px 0;">✅ ACCÈS AUTORISÉ</h3>
                <p style="color: #00ff80; font-size: 18px; margin: 10px 0;"><strong>VALIDÉ</strong></p>
                <p><strong>Nom :</strong> ${soldat.nom}</p>
                <p><strong>Grade :</strong> ${soldat.grade}</p>
                <p><strong>Promotion :</strong> ${soldat.promotion}</p>
                <p style="color: #00ff80;"><strong>${soldat.statut}</strong></p>
            </div>`;
    } else {
        resultDiv.innerHTML = `
            <div style="background: rgba(255, 50, 50, 0.1); border: 1px solid #ff3333; padding: 15px; border-radius: 4px; text-align: center;">
                <h3 style="color: #ff3333; margin: 0 0 10px 0;">❌ ACCÈS REFUSÉ</h3>
                <p style="color: #ff6666; font-size: 17px;">Nom non reconnu ou formation non validée</p>
                <p style="color: #ff9999;">"${input}"</p>
            </div>`;
    }
}
</script>
