# EQ-E1 — Compensation numérique de la phase des capteurs de courant

**Mesures citables — version du 2026-11-13.** Tous les chiffres de ce document sont copiés du dossier exécutif EQ-E1 et de ses fichiers de données. Chacun porte sa date et son unité. Aucun chiffre n'a été arrondi au-delà de ce que le dossier écrit.

## 1. Ce que fait la méthode

Le compteur d'énergie électronique mesure la température de son capteur de courant et la fréquence du réseau, convertit chacune de ces deux grandeurs en degrés de phase par une relation prédéterminée, additionne les deux corrections, puis retarde la sortie du processeur de la valeur obtenue. La correction est numérique et s'applique dans le compteur, pas dans un circuit analogique.

Ce document ne donne ni les coefficients, ni les équations, ni le code. Il décrit ce qui a été mesuré, comment, et avec quelles limites.

## 2. Ce qui est mesuré et ce qui ne l'est pas

**Mesuré, en simulation.** Un banc Monte-Carlo compare deux compteurs : un compteur étalonné une seule fois en usine, et le même compteur avec la compensation. Chaque cellule repose sur 21 graines × 1 000 capteurs, soit 21 000 capteurs simulés. Les imperfections de capteur (pentes ±10 %, non-linéarité, sonde décalée, bruit) sont des hypothèses H1–H7, pas des mesures.

**Non mesuré.** Aucun essai normalisé IEC n'a été réalisé. Aucune mesure sur un vrai transformateur de courant, ni sur un compteur physique. Les bancs de débit mesurent des temps de calcul, pas une supériorité métrologique.

## 3. Chiffres clés

| Réseau · facteur de puissance | Étalonnage usine seul (médiane de la pire erreur) | Avec compensation (médiane) | Date / source |
|---|---|---|---|
| 50 Hz · PF 0,5 | 3,36 % | 0,281 % | recalcul sur 21 graines ; dossier révisé le 2026-11-13 |
| 50 Hz · PF 0,8 | 1,46 % | 0,12 % | données du 2026-11-05 |
| 60 Hz · PF 0,5 | 3,08 % | 0,27 % | données du 2026-11-05 |
| 60 Hz · PF 0,8 | 1,34 % | 0,12 % | données du 2026-11-05 |

- La pire erreur est divisée par au moins 7 pour 95 % des capteurs simulés dans les quatre cellules. Le re-compte multi-graines à 50 Hz / PF 0,5 donne × 7,39, avec 96,98 % des capteurs à × 7 ou plus (dossier révisé le 2026-11-13).
- Témoin « zéro » : compensation forcée nulle, 0 % d'écart sur 3 000 capteurs par cellule, soit 12 000 lignes, écart maximal 0 (données du 2026-11-05).
- Débit : 531 025,17 mesures/s en moyenne sur 5 runs de 200 000 mesures, variation 0,70 % (banc court ; la date du banc court est fournie avec le dossier).

## 4. Limites, y compris défavorables

- Les imperfections de capteur sont supposées. Le gain dépend donc en partie des hypothèses du banc.
- L'ajout 2026 (étalonnage individuel) divise l'erreur par 5,6 à 50 Hz et 5,3 à 60 Hz : 0,0507 % contre 0,2819 % à 50 Hz, 0,0504 % contre 0,2682 % à 60 Hz. Mais sur des capteurs sans défaut propre, il fait moins bien : 0,0506 % contre 0,0314 % pour la compensation seule à 50 Hz. Le gain vient donc en partie de la forme du défaut simulé.
- Les bancs de débit ne prouvent aucune supériorité : ce sont des temps de calcul.
- Le statut juridique du brevet source est lu sur une page d'agrégateur archivée et reste à confirmer au registre officiel. Aucun avis juridique n'est fourni.

## 5. Comment reproduire

Le colis contient le protocole, les données brutes, les clés de recalcul et un manifeste SHA-256 (`MANIFESTE.sha256`). Le modèle exécutable passe 71 tests sur 71. Les fichiers de résultats et les données brutes sont fournis pour être rejoués ; chaque chiffre ci-dessus renvoie aux lignes correspondantes du dossier.

## 6. Fiche publique et contact

- Fiche : https://edgequantum65.fr/fiches/eq-e1
- Contact : https://edgequantum65.fr/contact
