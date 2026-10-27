# Analyse statistique, calibration et optimisation

## Ce que les données permettent de faire

Les résultats disponibles contiennent cinq réplications pour chacun des trois scénarios : temps de service moyen de 3,0, 4,0 et 4,5 minutes. Cet échantillon est limité : les calculs ci-dessous sont donc exploratoires. Ils servent à mesurer une tendance et son incertitude, pas à annoncer une différence définitive entre scénarios.

Les valeurs brutes sont conservées dans `results/raw_results.csv`. Les indicateurs sont le nombre de pièces terminées, la longueur moyenne de la file et l'utilisation moyenne de la station.

## 1. Moyenne, écart-type et erreur standard

Pour un indicateur $x$ mesuré sur $n=5$ réplications, la moyenne est :

$$
\bar{x}=\frac{1}{n}\sum_{r=1}^{n}x_r
$$

L'écart-type expérimental mesure la dispersion des résultats :

$$
s=\sqrt{\frac{\sum_{r=1}^{n}(x_r-\bar{x})^2}{n-1}}
$$

L'erreur standard mesure l'incertitude sur la moyenne estimée :

$$
SE=\frac{s}{\sqrt{n}}
$$

Exemple, pour les pièces terminées à 3,0 minutes :

$$
\bar{N}=\frac{107+113+86+103+88}{5}=99{,}40
$$

$$
s_N=11{,}887,\qquad
SE_N=\frac{11{,}887}{\sqrt{5}}=5{,}316
$$

| Temps de service | Pièces : moyenne ; s ; SE | File : moyenne ; s ; SE | Utilisation : moyenne ; s ; SE |
|---:|---:|---:|---:|
| 3,0 min | 99,40 ; 11,89 ; 5,32 | 1,032 ; 0,433 ; 0,194 | 0,666 ; 0,100 ; 0,045 |
| 4,0 min | 92,40 ; 11,46 ; 5,12 | 2,072 ; 0,825 ; 0,369 | 0,780 ; 0,031 ; 0,014 |
| 4,5 min | 94,60 ; 7,77 ; 3,47 | 2,942 ; 1,801 ; 0,805 | 0,832 ; 0,109 ; 0,049 |

## 2. Quartiles et médiane

Après tri des cinq valeurs, la convention retenue est : $Q_1$ = 2e valeur, médiane = 3e valeur et $Q_3$ = 4e valeur. Les quartiles, les valeurs minimales et maximales sont détaillés dans `results/summary.md`.

Ils complètent la moyenne : par exemple, la file moyenne au scénario 4,5 min possède une moyenne de 2,942 mais un écart-type de 1,801. Cette dispersion importante montre que cinq exécutions ne donnent pas encore une estimation très stable.

## 3. Intervalle de confiance de Student à 95 %

Comme la variance réelle est inconnue et que l'échantillon est petit, on utilise la loi de Student :

$$
\mathrm{IC}_{95} = \bar{x} \pm t_{0.975,\,n-1}\frac{s}{\sqrt{n}}
$$

Ici, $n=5$, donc 4 degrés de liberté :

$$
t_{0.975,\,4} \approx 2.776
$$

Pour les pièces terminées à 3,0 minutes :

$$
99.40 \pm 2.776 \times \frac{11.887}{\sqrt{5}}
\approx 99.40 \pm 14.76
$$

L'intervalle de confiance est donc approximativement :

$$
\mathrm{IC}_{95} \approx [84.64,\,114.16]
$$

Les intervalles des trois indicateurs sont publiés dans `results/summary.md`. Ils sont larges pour plusieurs mesures, ce qui confirme la prudence nécessaire. Le chevauchement de deux intervalles n'est pas un test statistique ; aucune différence significative n'est déclarée dans ce dépôt.

## 4. Lecture des résultats disponibles

Sur les cinq réplications par scénario, la file moyenne passe de 1.032 à 2.072 puis 2.942, et l'utilisation passe de 66.6 % à 78.0 % puis 83.2 %. Cette évolution est cohérente avec une station dont le temps de traitement augmente.

La production moyenne varie de 99.40 à 92.40 puis 94.60 pièces. Avec ce faible échantillon et des entrées aléatoires, on ne peut pas conclure qu'un service plus lent améliore la production.

## 5. Protocole de 30 réplications

La prochaine campagne utilisera 30 réplications par scénario, soit 90 exécutions. Pour chaque ligne du CSV, enregistrer : scénario, numéro de réplication, graine, paramètres et trois indicateurs.

Le réglage doit rester en mode **Random seed**, avec conservation des graines réellement utilisées. Des graines distinctes et traçables sont nécessaires pour soutenir l'hypothèse d'indépendance.

Avec $n=30$, l'intervalle de confiance devient :

$$
\mathrm{IC}_{95}
=
\bar{x} \pm t_{0.975,\,29}\frac{s}{\sqrt{30}}
$$

Le coefficient de Student correspondant est :

$$
t_{0.975,\,29} \approx 2.045
$$

Chaque graphique devra présenter la moyenne et une barre d'incertitude correspondant à la demi-largeur de cet intervalle. Les résultats bruts CSV doivent toujours être publiés avant les tableaux et graphiques calculés.

## 6. Calibration : méthode proposée

La calibration rapproche le modèle de données réelles comparables sur 480 minutes. Il faut notamment des mesures de production, de file ou d'attente, d'utilisation, d'arrêts et des règles de travail.

En l'absence de données réelles, aucune calibration réelle ne doit être annoncée. Tout exemple synthétique doit être explicitement identifié comme fictif.

Un premier vecteur de paramètres est :

$$
\theta = (\mathrm{meanArrivalMin},\,\mathrm{meanServiceMin})
$$

Pour les indicateurs $k=1,\ldots,K$, une fonction objectif pondérée possible est :

$$
J(\theta)
=
\sum_{k=1}^{K}
w_k
\left(
\frac{
\bar{y}^{\mathrm{sim}}_k(\theta)-y^{\mathrm{obs}}_k
}{
a_k
}
\right)^2
$$

où :

- $y^{\mathrm{obs}}_k$ est la mesure réelle ;
- $\bar{y}^{\mathrm{sim}}_k(\theta)$ est la moyenne simulée sur 30 réplications ;
- $w_k$ est un poids justifié ;
- $a_k$ est une échelle, par exemple une tolérance métier ou un écart-type observé.

Cette normalisation évite qu'un indicateur exprimé en nombre de pièces domine mécaniquement les autres.

La calibration retient le vecteur $\theta$ qui minimise $J$, puis vérifie la solution sur des données réelles différentes de celles utilisées pour l'ajustement.

## 7. Optimisation après calibration

Après calibration, une recherche paramétrique est adaptée au modèle : elle est simple, transparente et ne demande pas de dérivées.

On peut, par exemple, choisir une configuration $z$ qui maximise la production :

$$
\max_{z} \; \bar{N}(z)
$$

sous les contraintes :

$$
\bar{Q}(z) \leq Q_{\max}
$$

$$
\bar{U}(z) \leq U_{\max}
$$

$$
z \in \mathcal{Z}
$$

Les variables $z$ peuvent inclure la capacité de file, le nombre de stations ou un temps de service cible. Les limites $Q_{\max}$, $U_{\max}$ et le domaine $\mathcal{Z}$ doivent provenir de contraintes opérationnelles réelles.

Chaque solution candidate doit être évaluée par 30 réplications, puis validée par un nouveau lot indépendant de 30 réplications. Une solution est robuste si elle respecte les contraintes et conserve son avantage lors de cette validation.

## Limites

Les cinq réplications actuelles sont insuffisantes pour valider le modèle, calibrer ses paramètres ou optimiser la station. Elles constituent une base de travail transparente.

La priorité est donc : 30 réplications par scénario, enregistrement des graines, export CSV et graphiques avec barres d'incertitude.

Les variables $z$ peuvent inclure la capacité de file, le nombre de stations ou un temps de service cible. Les limites $Q_{\max}$, $U_{\max}$ et le domaine $\mathcal{Z}$ doivent provenir de contraintes opérationnelles réelles.

Chaque solution candidate doit être évaluée par 30 réplications, puis validée par un nouveau lot indépendant de 30 réplications. Une solution est robuste si elle respecte les contraintes et conserve son avantage lors de cette validation.

## Limites

Les cinq réplications actuelles sont insuffisantes pour valider le modèle, calibrer ses paramètres ou optimiser la station. Elles constituent une base de travail transparente.

La priorité est donc : 30 réplications par scénario, enregistrement des graines, export CSV et graphiques avec barres d'incertitude.
