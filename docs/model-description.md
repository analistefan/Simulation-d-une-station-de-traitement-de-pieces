# Description du modèle

## Idée générale

Le projet AnyLogic représente une station unique qui reçoit des pièces, les laisse attendre si la station est occupée, les traite, puis les envoie vers la sortie.

```text
srcPieces (Source) -> queueMachine (Queue) -> delayMachine (Delay) -> sinkFinished (Sink)
```

Cette chaîne est celle qui apparaît directement dans le fichier du modèle.

## Paramètres et logique observés

| Élément | Ce qui est défini dans le projet |
|---|---|
| `meanArrivalMin` | Paramètre, valeur par défaut : 5,0 |
| `meanServiceMin` | Paramètre, valeur par défaut : 3,0 |
| `srcPieces` | Crée les pièces avec `exponential(1.0 / meanArrivalMin)` comme temps entre arrivées, en minutes |
| `queueMachine` | File d'attente ; la collecte des statistiques est activée |
| `delayMachine` | Poste de traitement avec `exponential(1.0 / meanServiceMin)`, en minutes ; la collecte des statistiques est activée |
| `sinkFinished` | Compte les pièces sorties puis les retire du système |

Les expressions sont reproduites telles qu'elles figurent dans le fichier AnyLogic. Cette documentation ne leur donne pas une interprétation supplémentaire qui ne serait pas vérifiable dans le modèle.

## Indicateurs suivis

| Indicateur | Expression AnyLogic | Sens |
|---|---|---|
| Pièces terminées | `sinkFinished.count()` | Nombre de pièces arrivées à la sortie à la fin de la simulation |
| Longueur moyenne de file | `queueMachine.statsSize.mean()` | Nombre moyen de pièces en attente au cours du temps |
| Utilisation moyenne | `delayMachine.statsUtilization.mean()` | Taux moyen d'occupation de l'élément Delay |

## Paramètres d'exécution

L'unité du modèle est la minute et l'horizon de l'expérience *Simulation* est de 480 minutes. Dans le fichier transmis, le réglage de génération aléatoire est le mode `Random seed` et la valeur affichée est 42.

Le fichier ne contient pas d'expérience automatique de variation de paramètres ou de réplications. Les cinq exécutions par scénario doivent donc être tracées explicitement dans le protocole et dans le fichier de résultats.
