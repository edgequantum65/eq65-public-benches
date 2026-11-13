# EQ-C1 — Répartition de jobs par l'historique d'exécution

**Mesures citables — version du 2026-11-05.** Tous les chiffres sont copiés du dossier EQ-C1 et de ses fichiers de données, avec leur date et leur unité.

## 1. Ce que fait la méthode

Le serveur de file conserve l'historique des jobs passés, retrouve un job ressemblant, prédit la ressource nécessaire et n'envoie le job qu'à un serveur capable de l'absorber, en choisissant celui de charge minimale. S'il n'existe aucun job ressemblant, la méthode se replie sur le serveur au ratio d'utilisation minimal.

Ce document ne donne ni le code, ni la mesure de similarité, ni les paramètres. Il décrit ce qui a été mesuré, comment, et avec quelles limites.

## 2. Ce qui est mesuré et ce qui ne l'est pas

**Mesuré, en simulation.** Un banc long de 348 lignes, 330 graines distinctes dont 329 appariables, sur 30 jours, compare l'historique à la mémoire déclarée. Un banc de déclaration imprécise (scénarios D1 à D4, 30 graines chacun) et une validation à 10 graines complètent le dispositif.

**Non mesuré.** Aucune mesure sur un vrai cluster. Aucun effet mesuré sur le taux de jobs interrompus faute de mémoire, qui est pourtant le bénéfice attendu. Les niveaux d'imprécision des scénarios D1 à D4 sont choisis par l'auteur du banc, non sourcés.

## 3. Chiffres clés

| Ce qui est comparé | Résultat | Date |
|---|---|---|
| Temps de séjour, historique contre mémoire déclarée | **+3,525 s** en moyenne, IC95 [+1,983 ; +5,068] ; l'historique gagne sur **89 des 329** graines distinctes | re-compté le 2026-11-01 |
| Violations mémoire quand la déclaration est exacte | **+1,854** [+1,445 ; +2,263] violation par graine ; 3 903 contre 3 293 violations cumulées sur 329 graines | dossier du 2026-11-05 |
| Erreur de prévision mémoire, déclaration imprécise | de **−7,7 Mo** [−13,6 ; −1,8] en D1 à **−262,5 Mo** [−276,0 ; −249,0] en D4 | dossier du 2026-11-05 |
| Violations mémoire, déclaration imprécise | réduites de façon significative dans **un seul** scénario, la sous-déclaration de 50 % (D3) : −8,13 [−10,09 ; −6,18] | dossier du 2026-11-05 |
| Temps contre le serveur le moins chargé | −5,8 % (5 runs) et −3,8 % (10 graines) ; meilleur sur 6 graines sur 10 | dossier du 2026-11-05 |

## 4. Limites, y compris défavorables

- **Le critère principal du dossier est défavorable** : sur le temps de séjour, l'historique fait moins bien que la simple mémoire déclarée, de 3,525 s en moyenne, et ne gagne que sur 89 graines distinctes sur 329.
- **Quand l'utilisateur déclare juste, la méthode provoque plus de violations mémoire** que la mémoire déclarée (+1,854 par graine).
- Le seul avantage mesuré est une erreur de prévision plus faible quand la déclaration est fausse ; il ne se traduit par moins de violations que dans le scénario de forte sous-déclaration D3. En D1, D2 et D4, l'intervalle de confiance coupe zéro.
- **Le critère du banc long a été fixé après le début du banc** : écrit le 2026-10-09, banc démarré le 2026-09-30, après un premier calcul des écarts. Les critères du banc « déclaration imprécise » ont, eux, été écrits avant, le 2026-10-10.
- Une graine (1047) n'a pas de contrepartie déclarée : elle vient d'une version antérieure du banc, ce qui laisse 329 graines appariables sur 330.
- Aucun résultat sur matériel réel, et aucun droit opposable : la demande n'a jamais été délivrée.
- Aucun avis juridique ; le relevé des brevets tiers date du 2026-09-23 et doit être refait à la date de l'achat.

## 5. Comment reproduire

Le colis contient le modèle exécutable des revendications 1 à 6, 50 tests automatisés, un `Dockerfile`, le protocole, les données brutes du banc long et des bancs de déclaration, ainsi que l'ablation `declared`. Chaque chiffre ci-dessus renvoie à la ligne correspondante du dossier.

## 6. Fiche publique et contact

- Fiche : https://edgequantum65.fr/fiches/eq-c1
- Contact : https://edgequantum65.fr/contact
