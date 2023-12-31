# Comment-d-masquer-les-fraudeurs-par-BNP-Paribas-PF

# Contexte

BNP Paribas Personal Finance est le n°1 du financement aux particuliers en France et en Europe au travers de ses activités de crédit à la consommation.

Filiale à 100% du groupe BNP Paribas, BNP Paribas Personal Finance compte plus de 20 000 collaborateurs et opère dans une trentaine de pays. Avec des marques comme Cetelem, Cofinoga ou encore Findomestic, l'entreprise propose une gamme complète de crédits aux particuliers disponibles en magasin, en concession automobile ou directement auprès des clients via ses centres de relation client et sur internet. BNP Paribas Personal Finance a complété son offre avec des produits d'assurance et d'épargne pour ses clients en Allemagne, Bulgarie, France et Italie. BNP Paribas Personal Finance a développé une stratégie active de partenariat avec les enseignes de distribution, les constructeurs et les distributeurs automobiles, les webmarchands, et d'autres institutions financières (banque et assurance), fondée sur son expérience du marché du crédit et sa capacité à proposer des services intégrés adaptés à l'activité et à la stratégie commerciale de ses partenaires. Il est aussi un acteur de référence en matière de crédit responsable et d'éducation budgétaire.

BNPP Personal Finance est, par nature, exposée au Risque de Crédit, et s'appuie fortement sur des modèles quantitatifs pour le gérer. La direction Central Risk Department s'assure de la pertinence des modèles de notations de risque utilisés par les entités locales et garantit un niveau élevé d'expertise en intégrant des nouvelles techniques de modélisation dans notre environnement.

L'équipe Credit Process Optimization fait partie du département Risk Personal Finance Credit Decision Process and Policies, elle contribue à la rationalisation et à l'optimisation du process risque de décision par une approche analytique. Nous soutenons les équipes Risk en local pour améliorer l'efficacité de leur process de décision crédit, y compris sur la partie fraude. Il s'agit de trouver le meilleur compromis entre la profitabilité, l'expérience client et les profils de risque.

La fraude est un problème majeur de plus en plus préoccupant pour les institutions financières du monde entier. Les criminels utilisent une grande variété de méthodes pour attaquer des organisations comme la nôtre, quels que soient les systèmes, les canaux, les process ou les produits.

Le développement de méthodes de détection de la fraude est stratégique et essentiel pour nous. Les fraudeurs s'avèrent toujours très créatifs et ingénieux pour normaliser leurs comportements et les rendre difficilement identifiables. Une contrainte s'ajoute à cette problématique, la faible occurence de la fraude dans notre population.

But
L'objectif de ce challenge est de trouver la meilleure méthode pour transformer et agréger les données relatives au panier client d'un de nos parteneraires pour détecter les cas de fraude.

En utilisant ces données panier, les fraudeurs pourront être détectés, et ainsi refusés dans le futur.

# Description des données
1. Base de données
La base contient une liste d'achats effectués chez notre partenaire que nous avons financés. Les informations décrivent exclusivement le contenu du panier.

Pour chaque observation de la base, il y a 147 colonnes dont 144 peuvent être regroupées en 6 catégories :

item,

cash_price,

make,

model,

goods_code,

Nbr_of_prod_purchas.

Le panier se décompose au maximum en 24 items. Par exemple, si un panier contient 3 items alors toutes les informations relatives à ces 3 items seront renseignées dans les colonnes item1, item2, item3, cash_price1, cash_price_2, cash_price3, make1, make2, make3, model1, model2, model3, goods_code1, goods_code2, goods_code3, Nbr_of_prod_purchas1, Nbr_of_prod_purchas2 et Nbr_of_prod_purchas3. Les variables restantes (celles avec un indice > 3) seront vides .

Un item correspond à un produit ou un regroupement de produits équivalents. Par exemple, si un panier contient 3 Iphones 14, alors ces 3 produits seront regroupés dans un seul item. Par contre, si le client achète 3 produits Iphone différents, alors nous considèrerons ici 3 items.

La variable Nb_of_items correspond au nombre d'items dans le panier, tandis que la somme des variables Nbr_of_prod_purchas correspond au nombre de produits.

L’indicatrice fraud_flag permet de savoir si l’observation a été identifiée comme frauduleuse ou non.

1.1. Description des variables en entrée (X)
Variable	Description	Exemple
ID (Num)	Identifiant unique	1
item1 à item24 (Char)	Catégorie du bien de l'item 1 à 24	Computer
cash_price1 à cash_price24 (Num)	Prix de l'item 1 à 24	850
make1 à make24 (Char)	Fabriquant de l'item 1 à 24	Apple
model1 à model24 (Char)	Description du modèle de l'item 1 à 24	Apple Iphone XX
goods_code1 à goods_code24 (Char)	Code de l'item 1 à 24	2378284364
Nbr_of_prod_purchas1 à Nbr_of_prod_purchas24 (Num)	Nombre de produits dans l'item 1 à 24	2
Nb_of_items (Num)	Nombre total d'items	7

1.2. Description de la variable de sortie (Y)
Variable	Description
ID (Num)	Identifiant unique
fraud_flag (Num)	Fraude = 1, Non Fraude = 0

1.3. Taille de la base
Taille : 115 988 observations, 147 colonnes.

Distribution de Y :

Fraude (Y=1) : 1 681 observations

Non Fraude (Y=0) : 114 307 observations

Le taux de fraude sur l'ensemble de la base est autour de 1.4%.

2. Echantillons
La méthode d'échantillonnage appliquée est un tirage aléatoire simple sans remise. Ainsi, 80% de la base initiale a été utilisée pour générer l'échantillon de training et 20% pour l'échantillon de test.

2.1. Echantillon d'entraînement
Taille : 92 790 observations, 147 colonnes.

Distribution de Y_train :

Fraude (Y=1) : 1 319 observations

Non Fraude (Y=0) : 91 471 observations

2.2. Echantillon de test
Taille : 23 198 observations, 147 colonnes.

Distribution de Y_test :

Fraude (Y=1) : 362 observations

Non Fraude (Y=0) : 22 836 observations

# Description du benchmark
Métrique d'évaluation
L'objectif est d'identifier une opération frauduleuse dans la population en prédisant un risque/probabilité de fraude. Par conséquent, la métrique à utiliser est l'aire sous la courbe Précision-Rappel, appelé également PR-AUC.

La courbe Précision-Rappel s'obtient en traçant la précision (
�
�
�
�
+
�
�
TP+FN
TP
​
  ) sur l'axe des ordonnées et le rappel (
�
�
�
�
+
�
�
TP+FP
TP
​
  ) sur l'axe des abcisses pour tout seuil de probabilité compris entre 0 et 1.

Cette métrique est appropriée pour évaluer correctement la performance d'un modèle sur la classe minoritaire dans le cadre d'une classification fortement déséquilibrée.

Le meilleur modèle correspondra à celui avec la valeur de PR-AUC la plus élevée.

Pour ce challenge, la PR-AUC sera estimée par la moyenne pondérées des précisions à chaque seuil avec le poids associé étant la variation du rappel entre le seuil précédent et le nouveau seuil :

PR-AUC
=
Σ
�
(
�
�
−
�
�
−
1
)
�
�
PR-AUC=Σ 
n
​
 (R 
n
​
 −R 
n−1
​
 )P 
n
​
  ,

où 
�
�
P 
n
​
  et 
�
�
R 
n
​
  sont les précisions et recall du nème seuil.

N.B. Cette implémentation correspond à la métrique average_precision_score de sklearn.

Par conséquent, votre fichier de submission devra avoir le format suivant :

Variable	Description
ID (Num)	Identifiant unique
fraud_flag (Num)	Probabilité estimée (décimale positive entre 0 et 1) pour la classe minoritaire (1). Plus la valeur est élevée, plus la probabilité est forte d'être une opération frauduleuse.

Vous pouvez utiliser les fichiers .csv Y_test_random et Y_test_benchmark pour vérifier le format attendu et la taille de votre fichier de submission pour ce challenge.

# Benchmarks
Benchmark 1 : 
PR-AUC
1
=
0
,
017
PR-AUC 
1
​
 =0,017
Le premier benchmark est naïf et considère un modèle qui prédit aléatoirement une probabilité entre 0 et 1.

Benchmark 2 : 
PR-AUC
2
=
0
,
14
PR-AUC 
2
​
 =0,14
Le second benchmark intègre plusieurs étapes de pré-processing et utilise un modèle de Machine Learning optimisé pour prédire le risque de fraude.
