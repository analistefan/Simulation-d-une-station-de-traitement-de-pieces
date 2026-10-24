# Synthèse statistique des résultats relevés

Tous les calculs de cette page proviennent uniquement de [raw_results.csv](raw_results.csv). Chaque scénario contient cinq réplications. Les intervalles sont des intervalles de confiance de Student à 95 %, avec (t_{0{,}975;4}=2{,}776).

La méthode, les formules et les précautions d'interprétation sont détaillées dans [../docs/analyse-statistique.md](../docs/analyse-statistique.md).

## Pièces terminées

| Temps de service moyen | Moyenne | Écart-type | Q1 | Médiane | Q3 | IC à 95 % |
|---:|---:|---:|---:|---:|---:|---:|
| 3,0 min | 99,40 | 11,89 | 88 | 103 | 107 | [84,64 ; 114,16] |
| 4,0 min | 92,40 | 11,46 | 85 | 86 | 98 | [78,17 ; 106,63] |
| 4,5 min | 94,60 | 7,77 | 91 | 93 | 93 | [84,96 ; 104,24] |

## Longueur moyenne de la file

| Temps de service moyen | Moyenne | Écart-type | Q1 | Médiane | Q3 | IC à 95 % |
|---:|---:|---:|---:|---:|---:|---:|
| 3,0 min | 1,032 | 0,433 | 0,82 | 0,87 | 0,91 | [0,494 ; 1,570] |
| 4,0 min | 2,072 | 0,825 | 1,41 | 2,10 | 2,10 | [1,047 ; 3,097] |
| 4,5 min | 2,942 | 1,801 | 1,54 | 2,79 | 3,11 | [0,706 ; 5,178] |

## Utilisation moyenne de la station

| Temps de service moyen | Moyenne | Écart-type | Q1 | Médiane | Q3 | IC à 95 % |
|---:|---:|---:|---:|---:|---:|---:|
| 3,0 min | 0,666 (66,6 %) | 0,100 | 0,60 | 0,63 | 0,74 | [0,541 ; 0,791] |
| 4,0 min | 0,780 (78,0 %) | 0,031 | 0,78 | 0,78 | 0,80 | [0,742 ; 0,818] |
| 4,5 min | 0,832 (83,2 %) | 0,109 | 0,73 | 0,85 | 0,92 | [0,697 ; 0,967] |

## Lecture simple

- Sur les valeurs relevées, la file moyenne et l'utilisation moyenne augmentent avec le temps de service.
- Les intervalles de confiance sont souvent larges : cinq réplications ne suffisent pas pour une conclusion solide.
- Le fait que deux intervalles se recouvrent ne constitue pas, à lui seul, un test statistique. Aucune différence significative n'est déclarée ici.
