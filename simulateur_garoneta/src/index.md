---
toc: false
---

```js
// je charge les tranches de revenus
const tranches = FileAttachment("/data/tranche_revenu.json").json()
const tarifs_forfait = FileAttachment("/data/tarifs_forfait.json").json()
```





<div class="grid grid-cols-2">
  <div>
    <img src="/Garoneta_logo3C.png"> 
  </div>
  <div>
    <h1>Simulateur de Frais de Scolarité - Jours de Présence au CLAE</h1>
    <h2> Année Scolaire 2024-2025 </h2>
  </div>
</div>

<div class="caution", label="Attention">La simulation est réalisée en local dans votre navigateur. Aucune information n'est communiquée à l'école.</div>




<div class="grid grid-cols-2">
  <div class="card">
  <h3> Informations familiales : </h3>
  ${formulaire}
  </div>  
  <div class="card">
  <h3> Périodes de CLAE envisagées : </h3>
  ${clae}
  <br></br>
  <h4>Le déjeuner comprend la CLAE ainsi que la cantine.</h4>
  </div>
<div class="card">
  <h3> Vos Frais de scolarité annuels sont estimés ainsi :  </h3>

<table>
  <tr>
    <td></td>
    <td>Calcul</td>
    <td>Total</td>
  </tr>
  <tr>
    <td>Adhésion Asso Garoneta</td>
    <td></td>
  </tr>
  <tr>
    <td>Adhésion Asso Cor D'oc</td>
    <td></td>
  </tr>

  <tr>
    <td>Participation  gestion CLAE/Frais scolarité</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Cotisation Fédération Régionale + Départementale</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Cotisation Confédération</td>
    <td></td>
    <td></td>
    </tr>
  <tr>
    <td>Forfait Papier</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Provision Classe Verte</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Cantine</td>
    <td></td>
    <td>${Math.round(36*jour_dejeuner*prix_repas_cantine * 100) / 100}</td>
  </tr>
  <tr>
    <td>CLAE / CLSH</td>
    <td></td>
    <td></td>
  </tr>

</table>
</div>
<div class="card">
<h3>A reporter sur l'attestation :</h3>
</div class="card">

<div class="card">
Vos revenus mensuels sont de ${revenu_mensuel}€, votre tranche de revenu définie par la mairie de Toulouse est ${tranche_revenu['tranche']} (correspondant aux revenus compris entre  ${tranche_revenu['min']}€ et ${tranche_revenu['max']}€). Eu égard à votre nombre d'enfants, vos tarifs de clae seront ${tranche_revenu['tranche']}${lettre}. Le prix d'un repas est ${prix_repas_cantine}€. 
</div>

</div>


```js
const formulaire = (Inputs.form({
  inscrits: Inputs.range([0, 8], {step: 1, label: "Nombre d'inscrit(s) en calandrette"}),
  enfants: Inputs.range([1, 8], {step: 1, label: "Nombre d'enfant(s) de la famille"}),
  revenu_annuel: Inputs.range([0, 120000], {step: 1000, label: "revenu fiscal de référence annuel des parents ou représentant légaux"}),
  residant_toulouse: Inputs.radio(["Oui", "Non"], {label: "Résidant à Toulouse", value: null, format: (x) => x ?? "Abstain"}),
  famille_monoparentale: Inputs.radio(["Oui", "Non"], {label: "Famille monoparentale", value: null, format: (x) => x ?? "Abstain"}, 'toto')
}));
const formulaire_values = Generators.input(formulaire);
```

```js
const clae = (Inputs.form({
  lundi: Inputs.checkbox(["matin", "déjeuner", "soir"], {label: "lundi"}),
  mardi: Inputs.checkbox(["matin", "déjeuner", "soir"], {label: "mardi"}),
  mercredi: Inputs.checkbox(["matin", "déjeuner", "soir"], {label: "mercredi"}),
  jeudi: Inputs.checkbox(["matin", "déjeuner", "soir"], {label: "jeudi"}),
  vendredi: Inputs.checkbox(["matin", "déjeuner", "soir"], {label: "vendredi"})
}));
const clae_values = Generators.input(clae);
```

```js
// je calcule le revenu mensuel de reference et la tranche de revenu
const revenu_mensuel = Math.floor(formulaire_values['revenu_annuel'] / 12)   
const tranche_revenu =  tranches.filter(function(v) {return (v.min <= revenu_mensuel) & (v.max> revenu_mensuel);})[0]
const lettre = ['A', 'B', 'C'][Math.min(formulaire_values['enfants'], 3)-1] 
const prix_repas_cantine =  tarifs_forfait.filter(function(v) {return (v.tranche ==tranche_revenu['tranche']) & (v.lettre == lettre);})[0]['Repas cantine']
```



```js
const jour_dejeuner = clae_values['lundi'].includes('déjeuner') + clae_values['mardi'].includes('déjeuner') + 
                      clae_values['mercredi'].includes('déjeuner') + clae_values['jeudi'].includes('déjeuner') + 
                      clae_values['vendredi'].includes('déjeuner')
```




