<!-- U.I.T - DESIGN PREMIUM 2027 -->
<div style="max-width: 920px; margin: 40px auto; font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; background: linear-gradient(180deg, #0a0a0a, #1a1a1a); color: #e0e0e0; padding: 40px 30px; border-radius: 20px; box-shadow: 0 20px 60px rgba(0, 200, 120, 0.15); border: 1px solid #00c080;">

  <!-- En-tête stylé sans image -->
  <div style="text-align: center; margin-bottom: 45px; position: relative;">
    <div style="font-size: 52px; font-weight: 900; letter-spacing: 8px; background: linear-gradient(90deg, #00ffaa, #00cc88); -webkit-background-clip: text; -webkit-text-fill-color: transparent; text-shadow: 0 0 40px rgba(0, 255, 170, 0.5);">U.I.T</div>
    <div style="color: #00c080; font-size: 15px; letter-spacing: 4px; margin-top: -8px; font-weight: 500;">UNITÉ D'INTRUSION TACTIQUE</div>
    <div style="color: #666; font-size: 13px; margin-top: 8px;">ARMÉE GLENDALE • SYSTÈME DE VÉRIFICATION TACTIQUE</div>
  </div>

  <!-- Section Vérification -->
  <div style="background: rgba(20, 20, 20, 0.95); border-radius: 16px; padding: 40px; border: 1px solid rgba(0, 192, 128, 0.3); margin-bottom: 35px; box-shadow: inset 0 0 30px rgba(0,0,0,0.6);">
    <h2 style="text-align: center; color: #00ffaa; margin-bottom: 30px; font-size: 24px; font-weight: 600;">VÉRIFICATION DE FORMATION</h2>
    
    <input type="text" id="nom" placeholder="NOM COMPLET DU SOLDAT" 
           style="width: 100%; padding: 20px; font-size: 18px; background: #111; border: 2px solid #00c080; color: white; border-radius: 12px; margin-bottom: 20px; outline: none; transition: all 0.3s;">
    
    <button onclick="verifier()" 
            style="width: 100%; padding: 20px; background: linear-gradient(90deg, #00ffaa, #00cc77); color: #000; font-size: 18px; font-weight: 700; border: none; border-radius: 12px; cursor: pointer; box-shadow: 0 8px 25px rgba(0, 255, 170, 0.3); transition: all 0.3s;">
            VÉRIFIER L'ACCÈS
    </button>
    
    <div id="result" style="margin-top: 35px; min-height: 180px;"></div>
  </div>

  <!-- Bouton Admin -->
  <div style="text-align: center;">
    <button onclick="demanderMotDePasse()" 
            style="background: rgba(30,30,30,0.9); color: #ffcc00; padding: 14px 40px; border: 2px solid #ffcc00; border-radius: 50px; cursor: pointer; font-size: 16px; font-weight: 600; box-shadow: 0 5px 20px rgba(255, 200, 0, 0.2);">
            🔐 ADMINISTRATION
    </button>
  </div>

  <!-- Panneau Admin -->
  <div id="adminPanel" style="display: none; margin-top: 40px; background: rgba(20,20,20,0.98); border-radius: 16px; padding: 40px; border: 1px solid #ffcc00;">
    <h2 style="color: #ffcc00; text-align: center; margin-bottom: 30px;">Administration U.I.T</h2>
    
    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 18px; margin-bottom: 30px;">
      <input type="text" id="newNom" placeholder="Nom complet" style="padding: 16px; background: #111; border: 1px solid #ffcc00; color: white; border-radius: 10px;">
      <input type="text" id="newGrade" placeholder="Grade" style="padding: 16px; background: #111; border: 1px solid #ffcc00; color: white; border-radius: 10px;">
      <input type="text" id="newPromo" placeholder="Promotion" style="padding: 16px; background: #111; border: 1px solid #ffcc00; color: white; border-radius: 10px;">
    </div>
    
    <button onclick="ajouterSoldat()" style="width: 100%; padding: 18px; background: #ffcc00; color: #000; font-weight: 700; border: none; border-radius: 12px; margin-bottom: 30px; cursor: pointer;">➕ AJOUTER SOLDAT</button>

    <h3 style="color: #ffcc00; margin-bottom: 15px;">Soldats Enregistrés</h3>
    <div id="listeSoldats" style="background: #111; padding: 20px; border-radius: 12px; max-height: 400px; overflow-y: auto; border: 1px solid #333;"></div>

    <div style="margin-top: 35px; text-align: center; display: flex; gap: 15px; justify-content: center; flex-wrap: wrap;">
      <button onclick="sauvegarder()" style="background:#00ffaa; color:#000; padding:14px 30px; border:none; border-radius:50px; cursor:pointer;">💾 Sauvegarder</button>
      <button onclick="resetData()" style="background:#d32f2f; color:white; padding:14px 30px; border:none; border-radius:50px; cursor:pointer;">🗑️ Réinitialiser</button>
      <button onclick="fermerAdmin()" style="background:#555; color:white; padding:14px 30px; border:none; border-radius:50px; cursor:pointer;">Fermer</button>
    </div>
  </div>
</div>

<script>
// === DONNÉES ===
let soldatsValides = JSON.parse(localStorage.getItem('soldatsValides')) || {
  "Kassano Ange": { nom: "Kassano Ange", grade: "Soldat", promotion: "2026" },
  "Mr Ritchy": { nom: "Mr Ritchy", grade: "Caporal", promotion: "2026" }
};

const PASSWORD = "Kassano@10";

// === ADMIN ===
function demanderMotDePasse() {
  const mdp = prompt("🔐 Mot de passe Administration :");
  if (mdp === PASSWORD) {
    document.getElementById("adminPanel").style.display = "block";
    afficherListe();
  } else {
    alert("❌ Mot de passe incorrect");
  }
}

function fermerAdmin() {
  document.getElementById("adminPanel").style.display = "none";
}

function afficherListe() {
  const div = document.getElementById("listeSoldats");
  div.innerHTML = "";
  Object.keys(soldatsValides).forEach(nom => {
    const s = soldatsValides[nom];
    const item = document.createElement("div");
    item.style = "padding: 16px; background: #1a1a1a; margin-bottom: 10px; border-radius: 10px; display: flex; justify-content: space-between; align-items: center;";
    item.innerHTML = `
      <span><strong>${s.nom}</strong> — ${s.grade} (${s.promotion})</span>
      <button onclick="supprimerSoldat('${nom}')" style="background:#d32f2f;color:white;border:none;padding:8px 16px;border-radius:8px;cursor:pointer;">Supprimer</button>
    `;
    div.appendChild(item);
  });
}

// === VÉRIFICATION ===
function verifier() {
  const input = document.getElementById("nom").value.trim();
  const result = document.getElementById("result");
  result.innerHTML = "";

  if (!input) {
    result.innerHTML = `<p style="color:#ffcc00; text-align:center; font-size:17px;">⚠️ Veuillez entrer un nom</p>`;
    return;
  }

  const soldat = soldatsValides[input] || Object.values(soldatsValides).find(s => s.nom.toUpperCase() === input.toUpperCase());

  if (soldat) {
    result.innerHTML = `
      <div style="background: rgba(0, 255, 170, 0.12); border: 2px solid #00ffaa; padding: 35px; border-radius: 16px; text-align: center;">
        <h2 style="color: #00ffaa; margin: 0 0 20px 0; font-size: 28px;">✅ ACCÈS AUTORISÉ</h2>
        <p style="font-size: 22px; margin: 15px 0;"><strong>${soldat.nom}</strong></p>
        <p style="font-size: 17px;">Grade : ${soldat.grade}<br>Promotion : ${soldat.promotion}</p>
      </div>`;
  } else {
    result.innerHTML = `
      <div style="background: rgba(211, 47, 47, 0.12); border: 2px solid #d32f2f; padding: 35px; border-radius: 16px; text-align: center;">
        <h2 style="color: #d32f2f; margin: 0 0 20px 0; font-size: 28px;">❌ ACCÈS REFUSÉ</h2>
        <p style="color: #ff7777; font-size: 17px;">"${input}" non reconnu</p>
      </div>`;
  }
}

// === Autres fonctions (ajouter, supprimer, etc.) ===
function ajouterSoldat() {
  const nom = document.getElementById("newNom").value.trim();
  const grade = document.getElementById("newGrade").value.trim() || "Soldat";
  const promo = document.getElementById("newPromo").value.trim() || "2026";
  if (!nom) return alert("Nom obligatoire");
  soldatsValides[nom] = { nom, grade, promotion: promo };
  afficherListe();
  document.getElementById("newNom").value = "";
  document.getElementById("newGrade").value = "";
  document.getElementById("newPromo").value = "";
}

function supprimerSoldat(nom) {
  if (confirm(`Supprimer ${nom} ?`)) {
    delete soldatsValides[nom];
    afficherListe();
  }
}

function sauvegarder() {
  localStorage.setItem('soldatsValides', JSON.stringify(soldatsValides));
  alert("💾 Sauvegardé avec succès");
}

function resetData() {
  if (confirm("Tout effacer ?")) {
    localStorage.removeItem('soldatsValides');
    soldatsValides = {};
    afficherListe();
  }
}

// Init
afficherListe();
</script>
