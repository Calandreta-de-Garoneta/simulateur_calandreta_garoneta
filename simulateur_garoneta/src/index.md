---
toc: false
---

```js
// je charge les tranches de revenus
const tranches = FileAttachment("/data/tranche_revenu.json").json()
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

```js
const informations_famille = view(Inputs.form({
  inscrits: Inputs.range([0, 8], {step: 1, label: "Nombre d'inscrit(s) en calandrette"}),
  enfants: Inputs.range([1, 8], {step: 1, label: "Nombre d'enfant(s) de la famille"}),
  revenu_annuel: Inputs.range([0, 120000], {step: 1000, label: "revenu fiscal de référence annuel des parents ou représentant légaux"}),
  residant_toulouse: Inputs.radio(["Oui", "Non"], {label: "Résidant à Toulouse", value: null, format: (x) => x ?? "Abstain"}),
  famille_monoparentale: Inputs.radio(["Oui", "Non"], {label: "Famille monoparentale", value: null, format: (x) => x ?? "Abstain"})
}));
```

```js
// je calcule le revenu mensuel de reference et la tranche de revenu
const revenu_mensuel = Math.floor(informations_famille['revenu_annuel'] / 12)   
const tranche_revenu =  tranches.filter(function(v) {return (v.min <= revenu_mensuel) & (v.max> revenu_mensuel);})[0]
```



Vos revenus mensuels sont de ${revenu_mensuel}€, votre tranche de revenu définie par la mairie de Toulouse est ${tranche_revenu['tranche']} (correspondant aux revenus compris entre  ${tranche_revenu['min']} et ${tranche_revenu['max']}).  


Vos Frais de scolarité annuels sont estimés ainsi : 