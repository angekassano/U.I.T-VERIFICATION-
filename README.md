<!-- === U.I.T VERIFICATION PLATFORM - DESIGN PRO === -->
<div style="max-width: 900px; margin: 30px auto; font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; color: #e0e0e0; background: #0f0f0f; padding: 30px; border-radius: 12px; box-shadow: 0 10px 30px rgba(0,0,0,0.6);">

  <!-- Logo + En-tête -->
  <div style="text-align: center; margin-bottom: 35px;">
    <img src="<img width="1500" height="2235" alt="image" src="https://github.com/user-attachments/assets/bbebe01a-0a23-417b-9f23-b653446d17a2" />
" alt="U.I.T Logo" 
         style="max-width: 360px; border-radius: 8px; box-shadow: 0 0 25px rgba(0, 180, 120, 0.3);">
    <h1 style="color: #00c080; margin: 15px 0 8px 0; font-size: 28px; font-weight: 600; letter-spacing: 1px;">UNITÉ D'INTRUSION TACTIQUE</h1>
    <p style="color: #888; font-size: 15px;">ARMÉE GLENDALE • Plateforme de Vérification Sécurisée</p>
  </div>

  <!-- Vérification -->
  <div style="background: #1a1a1a; border-radius: 12px; padding: 35px; border: 1px solid #2a2a2a; margin-bottom: 30px;">
    <h2 style="color: #00c080; text-align: center; margin-bottom: 25px; font-size: 22px;">Vérification de Formation</h2>
    
    <input type="text" id="nom" placeholder="Entrez le nom complet du soldat" 
           style="width: 100%; padding: 18px; background: #252525; border: 1px solid #00c080; color: white; font-size: 17px; border-radius: 8px; margin-bottom: 20px; outline: none;">
    
    <button onclick="verifier()" 
            style="width: 100%; padding: 18px; background: #00c080; color: #000; font-weight: 700; font-size: 17px; border: none; border-radius: 8px; cursor: pointer; transition: all 0.3s;">
            VÉRIFIER L'ACCÈS
    </button>
    
    <div id="result" style="margin-top: 30px; min-height: 160px;"></div>
  </div>

  <!-- Bouton Admin -->
  <div style="text-align: center; margin: 20px 0;">
    <button onclick="demanderMotDePasse()" 
            style="background: #1f1f1f; color: #ffd700; padding: 12px 32px; border: 1px solid #ffd700; border-radius: 8px; cursor: pointer; font-size: 15px;">
            🔐 Accès Administration
    </button>
  </div>

  <!-- Panneau Admin -->
  <div id="adminPanel" style="display: none; background: #1a1a1a; border-radius: 12px; padding: 35px; border: 1px solid #ffd700;">
    <h2 style="color: #ffd700; text-align: center; margin-bottom: 25px;">Administration U.I.T</h2>
    
    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 15px; margin-bottom: 25px;">
      <input type="text" id="newNom" placeholder="Nom complet" style="padding: 14px; background: #252525; border: 1px solid #ffd700; color: white; border-radius: 8px;">
      <input type="text" id="newGrade" placeholder="Grade" style="padding: 14px; background: #252525; border: 1px solid #ffd700; color: white; border-radius: 8px;">
      <input type="text" id="newPromo" placeholder="Promotion" style="padding: 14px; background: #252525; border: 1px solid #ffd700; color: white; border-radius: 8px;">
    </div>
    
    <button onclick="ajouterSoldat()" 
            style="width: 100%; padding: 16px; background: #ffd700; color: #000; font-weight: 700; border: none; border-radius: 8px; margin-bottom: 25px; cursor: pointer;">
            ➕ Ajouter le Soldat
    </button>

    <h3 style="color: #ffd700; margin-bottom: 12px;">Soldats Enregistrés</h3>
    <div id="listeSoldats" style="background: #252525; padding: 20px; border-radius: 8px; max-height: 380px; overflow-y: auto; border: 1px solid #444;"></div>

    <div style="margin-top: 25px; text-align: center; display: flex; gap: 12px; justify-content: center; flex-wrap: wrap;">
      <button onclick="sauvegarder()" style="background:#00c080; color:#000; padding:12px 28px; border:none; border-radius:8px; cursor:pointer;">💾 Sauvegarder</button>
      <button onclick="resetData()" style="background:#d32f2f; color:white; padding:12px 28px; border:none; border-radius:8px; cursor:pointer;">🗑️ Réinitialiser</button>
      <button onclick="fermerAdmin()" style="background:#555; color:white; padding:12px 28px; border:none; border-radius:8px; cursor:pointer;">Fermer</button>
    </div>
  </div>
</div>

<script>
// Données
let soldatsValides = JSON.parse(localStorage.getItem('soldatsValides')) || {
  "Kassano Ange": { nom: "Kassano Ange", grade: "Soldat", promotion: "2026" },
  "Mr Ritchy": { nom: "Mr Ritchy", grade: "Caporal", promotion: "2026" }
};

const PASSWORD = "Kassano@10";

// Fonctions Admin
function demanderMotDePasse() {
  const mdp = prompt("🔐 Entrez le mot de passe administrateur :");
  if (mdp === PASSWORD) {
    document.getElementById("adminPanel").style.display = "block";
    afficherListe();
  } else {
    alert("❌ Mot de passe incorrect.");
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
    item.style = "padding: 14px; background: #1f1f1f; margin-bottom: 8px; border-radius: 8px; display: flex; justify-content: space-between; align-items: center;";
    item.innerHTML = `
      <span><strong>${s.nom}</strong> — ${s.grade} (${s.promotion})</span>
      <button onclick="supprimerSoldat('${nom}')" style="background:#d32f2f; color:white; border:none; padding:6px 14px; border-radius:6px; cursor:pointer;">Supprimer</button>
    `;
    div.appendChild(item);
  });
}

// Vérification
function verifier() {
  const input = document.getElementById("nom").value.trim();
  const result = document.getElementById("result");
  result.innerHTML = "";

  if (!input) {
    result.innerHTML = `<p style="color:#ffaa00; text-align:center; font-size:16px;">⚠️ Veuillez entrer un nom complet</p>`;
    return;
  }

  const soldat = soldatsValides[input] || Object.values(soldatsValides).find(s => s.nom.toUpperCase() === input.toUpperCase());

  if (soldat) {
    result.innerHTML = `
      <div style="background: rgba(0, 192, 128, 0.15); border: 2px solid #00c080; padding: 28px; border-radius: 12px; text-align: center;">
        <h2 style="color: #00c080; margin: 0 0 16px 0;">✅ ACCÈS AUTORISÉ</h2>
        <p style="font-size: 20px; margin: 12px 0;"><strong>${soldat.nom}</strong></p>
        <p style="font-size: 16px;">Grade : ${soldat.grade}<br>Promotion : ${soldat.promotion}</p>
      </div>`;
  } else {
    result.innerHTML = `
      <div style="background: rgba(211, 47, 47, 0.15); border: 2px solid #d32f2f; padding: 28px; border-radius: 12px; text-align: center;">
        <h2 style="color: #d32f2f; margin: 0 0 16px 0;">❌ ACCÈS REFUSÉ</h2>
        <p style="color: #ff7777;">"${input}" n'est pas enregistré ou n'a pas validé la formation.</p>
      </div>`;
  }
}

// Ajout / Suppression
function ajouterSoldat() {
  const nom = document.getElementById("newNom").value.trim();
  const grade = document.getElementById("newGrade").value.trim() || "Soldat";
  const promo = document.getElementById("newPromo").value.trim() || "2026";

  if (!nom) return alert("Le nom est obligatoire");
  
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
  alert("✅ Données sauvegardées");
}

function resetData() {
  if (confirm("Tout supprimer ? Action irréversible.")) {
    localStorage.removeItem('soldatsValides');
    soldatsValides = {};
    afficherListe();
  }
}

// Init
afficherListe();
</script>
