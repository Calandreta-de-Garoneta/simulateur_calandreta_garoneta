---
toc: false
---

```js
// je charge les tranches de revenus
const tranches = FileAttachment("/data/tranche_revenu.json").json()
const tarifs_actes = FileAttachment("/data/tarifs_actes.json").json()
const semaines = 36 
const lmjv = ['lundi', 'mardi', 'jeudi', 'vendredi']
const lmmjv = ['lundi', 'mardi', 'mercredi', 'jeudi', 'vendredi']
const cout_unitaire_asso_garoneta = 10
const cout_unitaire_cor_doc = 2
const cotisation_federation_regionale = 10
const cotisation_federation_departementale = 3

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
    <h3>Barême de tarification CLAE et Cantine</h3>

  Vos revenus mensuels sont de ${revenu_mensuel}€, votre tranche de revenu définie par la mairie de Toulouse est ${tranche_revenu['tranche']} (correspondant aux revenus compris entre  ${tranche_revenu['min']}€ et ${tranche_revenu['max']}€). Eu égard à votre nombre d'enfants, vos tarifs de CLAE et cantine seront ${tranche_revenu['tranche']}${lettre}.

<table>
  <tr>
    <td></td>
    <td>Coût unitaire</td>
    <td>Coût total</td>
  </tr>
  <tr>
    <td>CLAE matin</td>
    <td>${cout_clae_matin} €</td>
    <td>${Math.round(cout_clae_matin*nb_clae_matin*semaines*100)/100} €</td>
  </tr>
  <tr>
    <td>CLAE midi</td>
    <td>${cout_clae_midi} €</td>
    <td>${Math.round(cout_clae_midi*nb_clae_midi*semaines*100)/100} €</td>
  </tr>
  <tr>
    <td>CLAE soir</td>
    <td>${cout_clae_soir} €</td>
    <td>${Math.round(cout_clae_soir*nb_clae_soir*semaines*100)/100} €</td>
  </tr>
  <tr>
    <td>CLSH (mercredi)</td>
    <td>A faire €</td>
    <td>A faire €</td>
  </tr>

  <tr>
    <td>Cantine</td>
    <td>${prix_repas_cantine}</td>
    <td>${prix_repas_cantine*nb_jours_cantine*semaines} €</td>
  </tr>  
</table>



  </div>


<div class="card">
  <h3> Vos Frais de scolarité annuels sont estimés ainsi :  </h3>




<table>
  <tr>
    <td></td>
    <td>Coût Total</td>
  </tr>
  <tr>
    <td>Adhésion Asso Garoneta</td>
    <td>${cout_asso_garoneta} €</td>
  </tr>
  <tr>
    <td>Adhésion Asso Cor D'oc</td>
    <td>${cout_asso_cor_dor} €</td>
  </tr>
  <tr>
    <td>Participation  gestion CLAE/Frais scolarité</td>
    <td></td>
  </tr>
  <tr>
    <td>Cotisation Fédération Régionale et Départementale</td>
    <td>${cout_cotisation_federation_regionale_et_departementale} €</td>
  </tr>
  <tr>
    <td>Cotisation Confédération</td>
    <td></td>
    </tr>
  <tr>
    <td>Forfait Papier</td>
    <td></td> 
  </tr>
  <tr>
    <td>Provision Classe Verte</td>
    <td></td>
  </tr>
  <tr>
    <td>Cantine</td>
    <td>${Math.round(prix_repas_cantine*nb_jours_cantine*semaines * 100) / 100}</td>
  </tr>
  <tr>
    <td>CLAE / CLSH</td>  
    <td></td>
  </tr>

</table>
</div>
<div class="card">
<h3>A reporter sur l'attestation :</h3>
</div class="card">

<div class="card">
 
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
const prix_repas_cantine =  tarifs_actes.filter(function(v) {return (v.tranche ==tranche_revenu['tranche']) & (v.lettre == lettre);})[0]['Repas cantine']

```



```js
const nb_jours_cantine = (lmmjv.map(d=>clae_values[d].includes('déjeuner'))).reduce((accumulator, current) => 
accumulator + current);

const nb_clae_matin =  (lmjv.map(d=>clae_values[d].includes('matin'))).reduce((accumulator, current) => 
accumulator + current);
const cout_clae_matin = tarifs_actes.filter(function(v) {return (v.tranche ==tranche_revenu['tranche']) & (v.lettre == lettre);})[0]['CLAÉ matin']

const nb_clae_soir =  (lmjv.map(d=>clae_values[d].includes('soir'))).reduce((accumulator, current) => 
accumulator + current);
const cout_clae_soir = tarifs_actes.filter(function(v) {return (v.tranche ==tranche_revenu['tranche']) & (v.lettre == lettre);})[0]['CLAÉ soir']

const nb_clae_midi =  (lmjv.map(d=>clae_values[d].includes('déjeuner'))).reduce((accumulator, current) => 
accumulator + current);
const cout_clae_midi = tarifs_actes.filter(function(v) {return (v.tranche ==tranche_revenu['tranche']) & (v.lettre == lettre);})[0]['CLAÉ midi']

const statut_mercredi = clae_values['mercredi'].length

const cout_asso_garoneta = (2 - (formulaire_values['famille_monoparentale']=="Oui")) * cout_unitaire_asso_garoneta
const cout_asso_cor_dor = (2 - (formulaire_values['famille_monoparentale']=="Oui")) * cout_unitaire_cor_doc
const cout_cotisation_federation_regionale_et_departementale = formulaire_values['inscrits']*(cotisation_federation_departementale + cotisation_federation_regionale)
```

```js
cout_unitaire_cor_doc
```