## Question

**Déterminer si la sévérité des peines prononcées, pour des délits semblables, par les juges varient en fonction du quartier de résidence du détenu à Paris.** 

--> visualiser spatialement les différences en produisant plusieurs cartes puis en les réconciliants
--> recours nécessaire à une analyse multivariée, définition de catégorie

# Préparation des données

### Relations

TBL_individu
- ID_individu
- Nom_individu
- Quartier_paris

TBL_detention
- Duree_detention

TBL_motifdetention
- Label_motifdetention

### Sélection des délits

Sélection de délits à partir des regroupement de catégories déjà constituées, choix de quatre catégories en fonction de leur effectif et de la pertinence de la comparaison (axe évasion et surveillance non pertinent)

10 résultats
- contestataire
- contravention
- crime de sang
- escroquerie
- évasion
- moeurs
- petits delits
- politique
- social
- surveillance

```sql
SELECT count(code1)
FROM TBL_motifdetention
WHERE code1 = 'moeurs'
```

- Petits délits
- escroquerie
- social
- contestataire

### Création de la table de données

```sql
SELECT a.ID_individu, a.ID_alpage_adresse, a.Num_quartier, a.Quartier_paris, b.Duree_detention, c.code1
FROM TBL_individu AS a, TBL_detention AS b, TBL_motifdetention as c
WHERE a.ID_individu = b.ID_individu_detention AND b.ID_detention = c.ID_detention
AND (c.code1 = 'Petits  délits' OR c.code1 = 'escroquerie' OR c.code1 = 'social' OR  c.code1 = 'contestataire')
```

Regroupement par quartier

```sql
SELECT a.ID_individu, a.ID_alpage_adresse, a.Num_quartier, a.Quartier_paris, b.Duree_detention, c.code1 
FROM TBL_individu AS a, TBL_detention AS b, TBL_motifdetention as c 
WHERE a.ID_individu = b.ID_individu_detention AND b.ID_detention = c.ID_detention AND (c.code1 = 'Petits délits' OR c.code1 = 'escroquerie' OR c.code1 = 'social' OR c.code1 = 'contestataire')
```



## Création des cartes

- pb adresses

- regroupement par arrondissement

- Classification de Jenks sur les durées

- légendes pour les effectifs

  ### 

![Moyenne](Moyenne.png)

![Contestataires](Contestataires.png)

![petits délits](petits délits.png)

![sociaux](sociaux.png)

![escroquerie](escroquerie.png)



## Résultats

Carte seulement pertinente pour l’analyse d’adjacence

## Limites

- Obligation de multiplier les cartes pour la comparaison
  - superposition des cartes qui pose des pbs de réalisation pratique (RVB, CMYN, sapin de Noël !)
  - ambiguïtés de la représentation en fonction de l’effectif
- Effectifs réduits, disparité statistique
- Catégories qui ne permettent pas de déterminer la gravité des délits 

## Analyse factorielle

Corrélation, en fonction de la nature des données statistiques opère des corrélation différente.

![CHAgnesManhattanWardPlanfactorielle](CHAgnesManhattanWardPlanfactorielle.svg)



http://analyse.univ-paris1.fr

Est-ce que à crime égal on est jugé plus sévèrement en fonction de son quartier d’origine.




