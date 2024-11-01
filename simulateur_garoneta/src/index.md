---
toc: false
---

```js
// je charge les tranches de revenus
const tranches = FileAttachment("/data/tranche_revenu.json").json()
const tarifs_actes = FileAttachment("/data/tarifs_actes.json").json()
const forfait_scolarite = FileAttachment("/data/forfait_scolarite.json").json()
const semaines = 36 
const lmjv = ['lundi', 'mardi', 'jeudi', 'vendredi']
const lmmjv = ['lundi', 'mardi', 'mercredi', 'jeudi', 'vendredi']
const cout_unitaire_asso_garoneta = 10
const cout_unitaire_cor_doc = 2
const cotisation_federation_regionale = 10
const cotisation_federation_departementale = 3
const cotisation_Conferation_trimestrielle = 14 
const forfait_papier = 6
const classe_verte_maternelle = 60
const classe_verte_primaire = 180
```

<div class="grid grid-cols-2">
  <div>
    <a href="https://calandretadegaroneta.org/"><img src="/Garoneta_logo3C.png"></a> 
    <h4> Année Scolaire 2024-2025 </h4>
  </div>
  <div>
    <h2>Simulateur de Frais de Scolarité - Jours de Présence au CLAE</h2>
    
  </div>
</div>

<div class="caution", label="Attention !">

- Le simulateur a une vocation indicative et fournit une estimation approximative des frais. **Ces estimations ne sont pas opposables, et les frais réels seront confirmés lors de l'inscription définitive**.
- La simulation est effectuée localement dans votre navigateur, **aucune information ne quitte votre navigateur**.
- Le simulateur ne prend pas en charge les familles ayant plus de 4 enfants inscrits. Au delà de 4 enfants, il n'y a  plus de changement tarifaire.
- Assurez-vous que le nombre d'inscrits est bien inférieur ou égal au nombre d'enfants. Si besoin prenez contact avec l'école.
- Veuillez consulter l'[aide](./aide) pour savoir comment trouver votre revenu de référence ou obtenir de plus amples informations sur les frais et la tarification. 
</div>

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

  Eu égard à votre nombre d'enfants et votre revenu de référence, vos [tarifs de CLAE et cantine](./aide) seront ${tranche_revenu}${lettre}.

<table>
  <tr>
    <td></td>
    <td>Coût unitaire</td>
    <td>Coût total</td>
  </tr>
  <tr>
    <td>CLAE matin</td>
    <td>${prix_clae_matin} €</td>
    <td>${cout_clae_matin} €</td>
  </tr>
  <tr>
    <td>CLAE midi</td>
    <td>${prix_clae_midi} €</td>
    <td>${cout_clae_midi} €</td>
  </tr>
  <tr>
    <td>CLAE soir</td>
    <td>${prix_clae_soir} €</td>
    <td>${cout_clae_soir} €</td>
  </tr>
  <tr>
    <td>CLSH (mercredi)</td>
    <td>${prix_clae_mercredi} €</td>
    <td>${cout_clae_mercredi} €</td>
  </tr>

  <tr>
    <td>Cantine</td>
    <td>${prix_repas_cantine}</td>
    <td>${cout_cantine} €</td>
  </tr>  
</table>



  </div>


<div class="card">
  <h3> Vos Frais de scolarité annuels sont estimés ainsi :  </h3>




<table>
  <tr>
    <td></td>
    <td>Coût</td>
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
    <td>${cout_forfait_scolarite} €</td>
  </tr>
  <tr>
    <td>Cotisation Fédération Régionale et Départementale</td>
    <td>${cout_cotisation_federation_regionale_et_departementale} €</td>
  </tr>
  <tr>
    <td>Cotisation Confédération</td>
    <td>${cout_cotisation_Conferation_trimestrielle} €</td>
    </tr>
  <tr>
    <td>Forfait Papier</td>
    <td>${cout_forfait_papier} €</td> 
  </tr>
  <tr>
    <td>Provision Classe Verte</td>
    <td>${cout_classe_verte} €</td>
  </tr>
  <tr>
    <td>Cantine</td>
    <td>${cout_cantine}</td>
  </tr>
  <tr>
    <td>CLAE / CLSH</td>  
    <td>${cout_total_clae} €</td>
  </tr>
  <tr>
    <td><b>Total</b></td>  
    <td>${cout_total} €</td>
  </tr>

</table>
</div>

<div class="card">

  <h3>A reporter sur l'attestation :</h3>
  <table>
    <tr>
     <td>Répartition des coûts</td>
     <td>Coût</td>
    </tr>
    <tr>
     <td>Frais de scolarité</td>
     <td>${frais_de_scolarite} €</td>
    </tr>
    <tr>
      <td>Frais de garde</td>
      <td>${frais_de_garde} €</td>
    </tr>
    <tr>
      <td>Frais de repas</td>
      <td>${cout_cantine} €</td>
    </tr>
    <tr>
      <td><b>Total </b></td>
      <td>${cout_total} €</td>
    </tr>


  </table>

Le règlement se fera :

<b>CLAE, FRAIS DE GESTION MENSUELLE, CANTINE </b>
- Une facture mensuelle entre septembre et juin (au réel)
- Une facture de régularisation en juillet

<b>ADHÉSION, SOUTIEN FÉDÉRATIONS, FORFAIT PAPIER</b>
- Une facture annuelle en septembre

Appel à provisions classes vertes se fera par Hello Asso

</div class="card">

<div class="card">
<h3>Répartition des frais :</h3>
${echart1}
</div>
</div>

```js
const formulaire = (Inputs.form({
  enfants: Inputs.range([1, 4], {step: 1, label: "Nombre d'enfant(s) de la famille"}),
  inscrits_primaire: Inputs.range([0, 3], {step: 1, label: "Nombre d'inscrit(s) en primaire calandrette"}),
  inscrits_maternelle: Inputs.range([0, 3], {step: 1, label: "Nombre d'inscrit(s) en maternelle calendrette"}),
  revenu_annuel: Inputs.range([0, 120000], {step: 1000, label: "revenu fiscal de référence annuel des parents ou représentant légaux"}),
  parents_separes: Inputs.toggle({label: "Parents séparés", value: false}),
  famille_monoparentale: Inputs.toggle({label: "Famille monoparentale", value: false})
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
const tranche_revenu_brut =  tranches.filter(function(v) {return (v.min <= revenu_mensuel) & (v.max> revenu_mensuel);})[0]['tranche']
const tranche_revenu = Math.max(tranche_revenu_brut - 1 * formulaire_values['parents_separes'],1)  ;
const lettre = ['A', 'B', 'C'][Math.min(formulaire_values['enfants'], 3)-1] 
const prix_repas_cantine =  tarifs_actes.filter(function(v) {return (v.tranche ==tranche_revenu) & (v.lettre == lettre);})[0]['Repas cantine']
```

```js
const inscrits = formulaire_values['inscrits_primaire'] + formulaire_values['inscrits_maternelle']
const nb_jours_cantine = (lmmjv.map(d=>clae_values[d].includes('déjeuner'))).reduce((accumulator, current) => 
accumulator + current);
const cout_cantine = Math.round(prix_repas_cantine*nb_jours_cantine*semaines * 100) / 100

const nb_clae_matin =  (lmjv.map(d=>clae_values[d].includes('matin'))).reduce((accumulator, current) => 
accumulator + current);
const prix_clae_matin = tarifs_actes.filter(function(v) {return (v.tranche ==tranche_revenu) & (v.lettre == lettre);})[0]['CLAÉ matin']
const cout_clae_matin = Math.round(prix_clae_matin*nb_clae_matin*semaines*100)/100

const nb_clae_soir =  (lmjv.map(d=>clae_values[d].includes('soir'))).reduce((accumulator, current) => 
accumulator + current);
const prix_clae_soir = tarifs_actes.filter(function(v) {return (v.tranche ==tranche_revenu) & (v.lettre == lettre);})[0]['CLAÉ soir']
const cout_clae_soir = Math.round(prix_clae_soir*nb_clae_soir*semaines*100)/100

const nb_clae_midi =  (lmjv.map(d=>clae_values[d].includes('déjeuner'))).reduce((accumulator, current) => 
accumulator + current);
const prix_clae_midi = tarifs_actes.filter(function(v) {return (v.tranche ==tranche_revenu) & (v.lettre == lettre);})[0]['CLAÉ midi']
const cout_clae_midi = Math.round(prix_clae_midi*nb_clae_midi*semaines*100)/100

let prix_clae_mercredi ;
if (clae_values['mercredi'].includes('matin') && clae_values['mercredi'].includes('soir')){
  prix_clae_mercredi = tarifs_actes.filter(function(v) {return (v.tranche ==tranche_revenu) & (v.lettre == lettre);})[0]["ALSH journée"]
}  else if (clae_values['mercredi'].includes('matin') && (!clae_values['mercredi'].includes('soir'))){
  prix_clae_mercredi = tarifs_actes.filter(function(v) {return (v.tranche ==tranche_revenu) & (v.lettre == lettre);})[0]["ALSH matin"]
}  else if ((!clae_values['mercredi'].includes('matin')) && (clae_values['mercredi'].includes('soir'))){
  prix_clae_mercredi = tarifs_actes.filter(function(v) {return (v.tranche ==tranche_revenu) & (v.lettre == lettre);})[0]["ALSH a.-m."]
} else {prix_clae_mercredi = 0}
const cout_clae_mercredi = Math.round(prix_clae_mercredi * semaines * 100) / 100

const cout_total_clae = Math.round((cout_clae_matin + cout_clae_midi + cout_clae_soir + cout_clae_mercredi)*100)/100

const cout_asso_garoneta = Math.round((2 - (formulaire_values['famille_monoparentale'])) * cout_unitaire_asso_garoneta * 100) / 100
const cout_asso_cor_dor = (2 - (formulaire_values['famille_monoparentale'])) * cout_unitaire_cor_doc
const cout_cotisation_federation_regionale_et_departementale = inscrits*(cotisation_federation_departementale + cotisation_federation_regionale)
const cout_cotisation_Conferation_trimestrielle = cotisation_Conferation_trimestrielle * 4 * inscrits
const cout_forfait_papier = forfait_papier * inscrits 
const cout_classe_verte = classe_verte_maternelle * formulaire_values['inscrits_maternelle'] + classe_verte_primaire * formulaire_values['inscrits_primaire']
const cout_forfait_scolarite = forfait_scolarite.filter(function(v) {return (v.tranche ==tranche_revenu) & (v.lettre == lettre);})[0][inscrits] * 12

const cout_total = Math.round((cout_asso_garoneta+cout_asso_cor_dor+cout_cotisation_federation_regionale_et_departementale+cout_cotisation_Conferation_trimestrielle+cout_forfait_papier+cout_classe_verte+cout_forfait_scolarite+ cout_cantine + cout_total_clae)*100)/100

const frais_de_scolarite =  Math.round((cout_asso_garoneta + cout_asso_cor_dor+ cout_cotisation_federation_regionale_et_departementale + cout_cotisation_Conferation_trimestrielle+ cout_forfait_papier + cout_classe_verte + 20 *12)*100)/100

const frais_de_garde = Math.round((cout_forfait_scolarite + cout_total_clae- 20*12)*100)/100

```



```js 
//ici je construit mon graph echart
const echart1 = html`<div style="width: ${width/2}px; height:400px;"></div>`

const myChart = echarts.init(echart1);

const option = {
  xAxis: {
    type: 'category',
    data: ['Scolarité', 'Garde', 'Repas']
  },
  yAxis: {
    type: 'value'
  },
  series: [
    {
      data: [frais_de_scolarite, frais_de_garde, cout_cantine],
      type: 'bar'
    }
  ]
};



myChart.setOption(option)
```


<style>
body p { 
    font-family: 'merriweatherregular' !important;
    font-weight: normal;
    font-size: .9rem !important;
    line-height: 1.8 !important;
    color:#444444
}
body strong {
    font-family: 'merriweatherbold' !important;	
}
body em {
   font-family: 'merriweatheritalic' !important; 
}
body a:hover{
    text-decoration: underline;
    text-decoration-skip: ink!important;
    color:#6f2200;
}
body a{
	/*text-decoration: underline!important;*/
}
p{
  -webkit-font-smoothing: antialiased!important;
  -moz-osx-font-smoothing: grayscale;
  font-family: 'merriweatherregular';
}
h1,h2,h3,h4,h5,h6 {
  letter-spacing: 0.05em !important;
  font-weight: normal !important;
}
h1 {
  font-family: oswaldmedium !important;
  text-transform: uppercase !important;
  text-align:center !important;
  font-size:2.5em!important;
  line-height:1.2em!important;
  color: #444444 !important;
  margin: 10px 0px 10px 0px !important;
}
.row .col.section-title h1 { 
  padding-top: 5px;
  padding-bottom: 5px;
}
.single #single-below-header {
  margin-bottom: 18px !important;
  }
h2 {
  font-family: oswaldmedium !important;
  text-transform: uppercase !important;
  font-size:1.6em!important;
  line-height:1.1em!important;
  color: #b54512 ;
  margin: 20px 0px 10px 0px !important;}
h3 {
  letter-spacing: 0.05em !important;
  font-family: oswaldregular !important;
  text-transform: uppercase !important;
  font-size:1.5em!important;
  line-height:1.2em!important;
  margin: 20px 0px 10px 0px !important;
}
.chapeau p { 
  font-family: inherit;
  color:#000000 !important;
  font-size: 1.4em !important;
  line-height: 1.8em !important;
}
.soustitre h2 {
  font-family: oswaldregular !important;
  text-transform: none!important;
  font-size:2.1em!important;
  line-height:1.1em!important;
  color: #3fbfeb ;
  margin: 20px 0px 5px 0px !important;}
}
.citation-box {
  background-color: #FFFFFF !important;
  padding: 40px !important;
  margin: 0px !important;
}
.citation-box p {
  font-family: merriweatheritalic !important;
  font-size:1.3em !important;
  color: #3b7386;
  background-color: #FFFFFF !important;
  padding: 40px !important;
  margin: 0 10% !important;
}
.container-wrap body{
  padding-top: 0px;
}
.page-header-no-bg {
  padding-top: 0px !important;
  margin-top: 0px !important;
}

</style>  