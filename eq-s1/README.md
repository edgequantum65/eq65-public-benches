# EQ-S1 — Réduction du coût de recherche du gestionnaire d'exception

**Mesures citables — version du 2026-11-13.** Tous les chiffres sont copiés du dossier exécutif EQ-S1 et de ses fichiers de données, avec leur date et leur unité. Aucun chiffre n'a été arrondi au-delà de ce que le dossier écrit.

## 1. Ce que fait la méthode

Le système mesure à l'exécution la fréquence des chemins d'exception. Seuls les chemins jugés chauds sont transformés à la compilation pour brancher directement vers le gestionnaire ; les chemins froids conservent la recherche classique. Deux techniques séparables ou combinables sont décrites : transformation du code à la compilation, et profil d'exécution avec décision au-delà d'un seuil.

Ce document ne donne ni le code, ni l'algorithme d'analyse, ni les seuils. Il décrit ce qui a été mesuré, comment, et avec quelles limites.

## 2. Ce qui est mesuré et ce qui ne l'est pas

**Mesuré.** Un banc de 168 runs sur 13 jours distincts, du 2026-10-18 au 2026-10-31, avec une seule empreinte de code et des critères V1 à V6. Le banc compare un interpréteur Python à pile équipé de la méthode et le même interpréteur sans elle.

**Non mesuré.** Aucune JVM réelle, aucun JIT, aucun code machine. Le banc ne mesure pas la performance d'une machine virtuelle industrielle ; il mesure la mécanique du modèle dans un interpréteur Python.

## 3. Chiffres clés

| Critère | Résultat | Verdict |
|---|---|---|
| V1 équivalence fonctionnelle | 0 écart sur `result`, `handled`, `uncaught`, `checksum`, toutes charges, tous runs | RÉUSSITE |
| V2 coût de recherche, chemin chaud | 0,000 contre 5,000 ; ratio 0,000 | RÉUSSITE |
| V3 temps par exception, chemin chaud | ratio des médianes 0,872, IC95 [0,868 ; 0,875] ; 9 169 ns contre 10 514 ns | **GAIN NON DÉMONTRÉ** (seuil 0,80) |
| V4 non-régression sans exception | ratio des médianes 0,996, IC95 [0,993 ; 1,000] | RÉUSSITE |
| V5 sélectivité, chemin froid | 0 site optimisé, 0 run avec écart | RÉUSSITE |
| V6 témoin sans exception | 0 valeur non nulle, 0 écart | RÉUSSITE |

Le code livré compte 8 fichiers (6 modules Python) et 17 tests verts. La preuve couvre donc l'équivalence, la sélectivité et l'absence de régression, mais **pas le gain de temps au seuil fixé**. Autrement dit : le gain de recherche est acquis, le gain de temps n'est pas démontré.

## 4. Limites, y compris défavorables

- **Le gain de temps n'est pas démontré** : 0,872 pour un seuil de réussite fixé à 0,80. Le dossier l'écrit comme un gain non démontré, pas comme un succès partiel.
- **Le gain de recherche V2 est acquis par construction** : dans la simulation, la variante optimisée n'interroge pas la table d'exception sur le chemin chaud. Ce chiffre décrit la mécanique du modèle, pas une performance mesurée sur une machine virtuelle.
- Aucune transposition à une JVM réelle, avec JIT et code machine, n'est fournie.
- Un run sur 168 (le premier, graine 229000) porte une empreinte de critères antérieure. Les verdicts sur les 167 runs homogènes sont identiques.
- La preuve de date (OTS) du dossier n'est pas posée à ce jour.
- Aucun avis juridique ; les brevets tiers relevés n'ont pas été analysés revendication par revendication.

## 5. Comment reproduire

Le colis contient le protocole, les critères V1 à V6, la commande de banc, les 168 lignes de données brutes, les fichiers de code et leurs tests. La trace journalière est recalculée sur les 168 runs, par jour, en médiane, avec la même statistique que le résultat publié.

## 6. Fiche publique et contact

- Fiche : https://edgequantum65.fr/fiches/eq-s1
- Contact : https://edgequantum65.fr/contact
