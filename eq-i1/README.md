# EQ-I1 — Transformée par tuiles à mémoire réduite

**Mesures citables — version du 2026-11-13.** Tous les chiffres sont copiés du dossier EQ-I1 et de ses fichiers de données, avec leur date et leur unité.

## 1. Ce que fait la méthode

La méthode réduit la mémoire de travail nécessaire pour transformer une image, sans effet de bord. La transformée est prédéfinie ; elle n'est pas apprise.

Ce document ne donne ni le code, ni la recette d'implémentation, ni les paramètres de dimensionnement. Il décrit ce qui a été mesuré, comment, et avec quelles limites.

## 2. Ce qui est mesuré et ce qui ne l'est pas

**Mesuré.** Un banc long de 168 runs sur 13 jours avec données, du 2026-10-18 au 2026-10-31 (14 jours calendaires), compare la méthode à la transformée pleine image sur chaque run, avec une seule empreinte de code. Un banc complémentaire du 2026-11-04 porte sur 3 photographies réelles (domaine public ; CC BY 2.0, attribution obligatoire), agrandies ×2 à ×2,4 par interpolation BICUBIC, puis découpées en 30 cadrages de 1024×1024 ; la mémoire y est tracée image par image avec `tracemalloc`, et le temps y a été mesuré hors `tracemalloc`.

**Non mesuré.** Aucune mesure sur ASIC ni sur cible embarquée. Les images du banc long sont simulées. Les temps sont ceux d'un programme Python sur PC.

## 3. Chiffres clés

| Critère | Résultat | Date |
|---|---|---|
| Mémoire dynamique mesurée (`tracemalloc`, 30 tirages) | 33,6 Mo → 8,5 Mo, soit ×3,95 | 2026-11-04 |
| Qualité (écart PSNR) | −0,0578 dB en moyenne, IC95 [−0,0784 ; −0,0372] dB, 168/168 | banc du 2026-10-18 au 2026-10-31 |
| Temps, images simulées (critère ≤ 1,5×) | 4,24× plus lente, critère non atteint 0/168 | banc du 2026-10-18 au 2026-10-31 |
| Photographies réelles | écart −0,1532 dB, IC95 [−0,2296 ; −0,0768] dB ; ratio de temps moyen 5,43× sur 30 cadrages (moyenne des ratios par cadrage ; le rapport des temps moyens, 2 290 ms / 428 ms, donne 5,35×), mesuré hors `tracemalloc` | 2026-11-04 |

## 4. Limites, y compris défavorables

- **Le critère de temps est raté sur tous les runs** (0/168) : la méthode est 4,24× plus lente. C'est le coût de la méthode sur ce banc.
- Ce ×3,95 compare le pic mémoire d'une réalisation qui garde une copie entière de l'image en entiers 64 bits (8 388 608 octets sur 8 512 819 mesurés) ; il ne mesure pas la cible mémoire annoncée.
- Aucun témoin « image constante » dans le banc long, et le débit binaire n'y est pas tracé : l'égalité de débit n'y est pas vérifiable. Le type `contours` donne 100 dB des deux côtés, une valeur de repli, pas une mesure de qualité.
- 7 revendications ne sont ni implémentées ni reliées au code, et les revendications système et produit programme ne sont pas réalisées en matériel.
- Le statut juridique est lu sur une page d'agrégateur ; la recherche de tiers n'est pas concluante et aucun avis juridique n'est fourni.

## 5. Comment reproduire

Le colis contient le protocole écrit le 2026-10-07, les 168 lignes de données brutes du banc long, les 30 lignes du banc photos et le tableau revendication → code → test. Les critères du banc principal ont été fixés avant l'essai ; ceux du banc photos ont été ajustés après un premier passage, et c'est écrit dans le dossier. Chaque mesure est fournie avec sa commande de recalcul.

## 6. Fiche publique et contact

- Fiche : https://edgequantum65.fr/fiches/eq-i1
- Contact : https://edgequantum65.fr/contact
