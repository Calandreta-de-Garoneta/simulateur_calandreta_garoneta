---
toc: false
---

<div class="grid grid-cols-2">
  <div>
  <img src="/Garoneta_logo3C.png"> 
  <h2> Année Scolaire 2024-2025 </h2>
  </div>
  <div> <h1>Simulateur de Frais de Scolarité - Jours de Présence au CLAE</h1></div>
</div>

Pour plus d'informations sur les 

```js
const rgb2 = view(Inputs.form({
  inscrits: Inputs.range([0, 8], {step: 1, label: "Nombre d'inscrit(s) en calandrette"}),
  enfants: Inputs.range([1, 8], {step: 1, label: "Nombre d'enfant(s) de la famille"}),
  revenus: Inputs.range([0, 100000], {step: 50, label: "Revenu mensuel de la famille"}),
  residant_toulouse: Inputs.radio(["Oui", "Non"], {label: "Résidant à Toulouse", value: null, format: (x) => x ?? "Abstain"}),
  famille_monoparentale: Inputs.radio(["Oui", "Non"], {label: "Famille monoparentale", value: null, format: (x) => x ?? "Abstain"})
}));
```



Vos Frais de scolarité annuels sont estimés ainsi : 

 
