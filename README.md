# 🧪 Méthodologie de génération des profils de charge

## 1. Principe général

La méthode consiste à générer des profils de charge synthétiques à l’échelle horaire pour différents types de consommateurs (industriels et résidentiels), en s’appuyant sur deux profils de référence : un jour ouvrable et un jour de week-end. Contrairement à une approche séquentielle où chaque jour dépend du précédent, cette méthode repose sur une logique de génération indépendante mais structurée, permettant une simulation rapide, cohérente et contrôlable.

## 2. Profils de référence

Deux profils initiaux sont utilisés comme base :

- **Profil ouvrable** : représentant un jour typique de semaine avec activité industrielle et résidentielle.
- **Profil week-end** : représentant un jour typique de fin de semaine avec activité industrielle réduite et usage résidentiel plus étalé.

Ces profils servent de point de départ pour générer l’ensemble des jours du mois, en alternant les jours ouvrables et les week-ends selon une structure hebdomadaire.

## 3. Génération stochastique

Chaque jour est généré à partir du profil de référence correspondant (ouvrable ou week-end), en appliquant :

- `apply_variation` : pour simuler les fluctuations naturelles de la demande par perturbation locale.
- `apply_random_series` : pour modéliser les plages horaires à forte variabilité à l’aide de séries aléatoires paramétrées (moyenne, écart-type).

Cette approche permet de conserver la structure typique des profils tout en introduisant une diversité statistique réaliste.

## 4. Structure temporelle

La simulation est organisée en trois niveaux :

- **Journée** : génération d’un jour complet à partir du profil de référence.
- **Semaine** : assemblage de 4 jours ouvrables et 2 jours de week-end.
- **Mois** : enchaînement de semaines jusqu’à atteindre le nombre exact de jours du mois, avec prise en compte des mois de 29, 30 ou 31 jours.

## 5. Avantages de l’approche

- **Simplicité et rapidité** : pas de dépendance séquentielle, donc génération parallèle possible.
- **Contrôle statistique** : les paramètres de variation peuvent être ajustés facilement pour tester différents scénarios.
- **Cohérence typologique** : chaque jour conserve les caractéristiques propres à son type (ouvrable ou week-end).