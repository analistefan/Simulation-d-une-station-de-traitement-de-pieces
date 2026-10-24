# Méthode expérimentale

## Plan utilisé pour les résultats publiés

Les résultats relevés correspondent à 15 exécutions :

- 5 réplications avec `meanServiceMin = 3,0` ;
- 5 réplications avec `meanServiceMin = 4,0` ;
- 5 réplications avec `meanServiceMin = 4,5`.

Le paramètre d'arrivée du modèle transmis est maintenu à 5,0 minutes. Pour chaque réplication, trois indicateurs sont relevés : le nombre de pièces terminées, la longueur moyenne de la file et l'utilisation moyenne.

## Démarche suivie

1. Reporter une ligne par réplication dans [../results/raw_results.csv](../results/raw_results.csv).
2. Séparer les lignes selon le temps moyen de service.
3. Calculer la moyenne, l'écart-type expérimental et les quartiles de chaque groupe.
4. Construire un intervalle de confiance de Student à 95 % si les réplications sont indépendantes.
5. Interpréter les écarts avec prudence, car il n'y a que cinq valeurs par scénario.

Les formules et les calculs numériques sont détaillés dans [analyse-statistique.md](analyse-statistique.md).

## Contrôles réalisés

- 15 valeurs ont été comptées : 5 pour chacun des 3 scénarios.
- Les valeurs d'utilisation sont toutes comprises entre 0 et 1.
- Les trois colonnes de résultats correspondent aux expressions suivies dans le modèle AnyLogic.
- L'horizon de 480 minutes, le paramètre d'arrivée à 5,0 minutes, les trois réglages de service et le mode `Random seed` avec valeur 42 ont été vérifiés dans le fichier `.alp`.
- Les moyennes, écarts-types, quartiles et intervalles publiés sont recalculés à partir du CSV brut.

## Ce qui reste à améliorer

Le modèle transmis ne documente pas les graines effectivement utilisées pour les cinq exécutions de chaque scénario. On ne peut donc pas démontrer, uniquement avec ce fichier et les notes manuscrites, que les 15 réplications sont indépendantes ou régénérer exactement toutes leurs valeurs.

La prochaine campagne doit enregistrer une graine par exécution, exporter les résultats bruts et utiliser un nombre de réplications plus grand. Trente réplications par scénario constituent un premier objectif pratique ; le bon nombre dépend ensuite de la précision recherchée et de la largeur des intervalles de confiance.
