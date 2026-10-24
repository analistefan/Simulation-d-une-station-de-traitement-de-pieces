# Analyse statistique des réplications

## Pourquoi ajouter cette étape ?

Une simulation aléatoire ne donne pas toujours le même résultat d'une exécution à l'autre. La moyenne est utile, mais elle ne suffit pas : il faut aussi regarder la dispersion des résultats et l'incertitude autour de la moyenne.

Ici, chaque scénario ne contient que (n = 5) réplications. Les résultats doivent donc être considérés comme exploratoires.

## 1. Moyenne

Pour un indicateur (x) observé sur (n) réplications :

\[
\bar{x}=\frac{1}{n}\sum_{r=1}^{n}x_r
\]

Exemple pour les pièces terminées du scénario à 3,0 minutes :

\[
\bar{N}=\frac{107+113+86+103+88}{5}=\frac{497}{5}=99{,}40
\]

## 2. Écart-type expérimental

L'écart-type mesure la dispersion des résultats autour de leur moyenne :

\[
s=\sqrt{\frac{\sum_{r=1}^{n}(x_r-\bar{x})^2}{n-1}}
\]

Le dénominateur est (n-1), car il s'agit de l'écart-type d'un échantillon. Un écart-type élevé indique que les cinq résultats sont assez dispersés.

## 3. Quartiles et médiane

Les quartiles donnent une lecture simple de la répartition des cinq valeurs, une fois triées. La convention utilisée ici est la convention usuelle française du rang :

- (Q_1) : rang (lceil n/4 \rceil) ;
- médiane : valeur centrale ;
- (Q_3) : rang (lceil 3n/4 \rceil).

Avec (n=5), (Q_1), la médiane et (Q_3) correspondent donc aux 2e, 3e et 4e valeurs triées. Cette convention est indiquée pour que les calculs soient entièrement reproductibles.

## 4. Intervalle de confiance de Student à 95 %

Lorsque la variance réelle est inconnue et que l'échantillon est petit, une première approximation de l'intervalle de confiance de la moyenne utilise la loi de Student :

\[
IC_{95\%}=\bar{x}\pm t_{0{,}975;\,n-1}\frac{s}{\sqrt{n}}
\]

Pour (n=5), il y a 4 degrés de liberté et (t_{0{,}975;4}\approx2{,}776).

Exemple pour les pièces terminées à 3,0 minutes :

\[
99{,}40\pm2{,}776\times\frac{11{,}887}{\sqrt{5}}
=99{,}40\pm14{,}76
\]

Ainsi :

\[
IC_{95\%}\approx[84{,}64\ ;\ 114{,}16]
\]

Cet intervalle est large, ce qui est normal avec seulement cinq réplications et une variabilité non négligeable.

## Conditions et prudence

La formule de Student suppose que les réplications sont indépendantes et que la moyenne d'échantillon peut être raisonnablement approximée par une loi normale. Avec cinq observations, ces conditions sont difficiles à vérifier. L'intervalle est donc une estimation pédagogique et exploratoire ; il ne faut pas l'utiliser pour affirmer qu'une différence entre scénarios est statistiquement significative.

## Prochaine étape recommandée

La suite la plus utile est de lancer au moins 30 réplications par scénario, en enregistrant la graine de chaque exécution et en exportant directement les résultats dans un CSV. Ensuite, il sera possible de recalculer les intervalles de confiance et d'ajouter des graphiques avec barres d'incertitude. Si les intervalles restent trop larges, il faudra augmenter davantage le nombre de réplications.
