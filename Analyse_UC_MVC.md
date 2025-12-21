# Analyse des Cas d'Utilisation - Démarche MVC

## Système d'évaluation des enseignants

---

## 📋 Cas d'utilisation sélectionnés

### 1. UC1 - Remplir une évaluation

**Justification du choix :** C'est le cas d'utilisation central du système pour les étudiants. Sans cette fonctionnalité, le système ne peut pas fonctionner. Elle inclut des aspects critiques comme l'anonymat et la compatibilité mobile.

### 2. UC6 - Visualiser le tableau de bord interactif

**Justification du choix :** C'est le cas d'utilisation le plus important pour les enseignants et administrateurs. Il permet de consulter les résultats, suivre l'évolution des performances et prendre des décisions basées sur les données.

---

## 🏗️ Architecture MVC appliquée

### Modèle MVC utilisé

```
┌─────────────────────────────────────────────────────────────┐
│                    COUCHE PRÉSENTATION                       │
│                         (Vue)                                │
│  - Interface utilisateur (Web/Mobile)                       │
│  - Gestion de l'affichage                                   │
│  - Composants graphiques interactifs                        │
└─────────────────────┬───────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────┐
│                    COUCHE MÉTIER                             │
│                    (Contrôleur)                              │
│  - Logique métier                                           │
│  - Validation des données                                   │
│  - Services (Anonymat, Notifications, Statistiques)         │
└─────────────────────┬───────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────┐
│                    COUCHE DONNÉES                            │
│                      (Modèle)                                │
│  - Accès aux données                                        │
│  - ORM / Requêtes SQL                                       │
│  - Persistance                                              │
└─────────────────────┬───────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────┐
│                  BASE DE DONNÉES                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 📊 UC1 - Remplir une évaluation

### Diagramme de séquence

**Fichier :** [Diagramme_Sequence_UC1_Remplir_Evaluation.puml](Diagramme_Sequence_UC1_Remplir_Evaluation.puml)

### Scénario idéal

**Description :** L'étudiant accède au formulaire d'évaluation, le remplit complètement et le soumet avec succès.

**Étapes principales :**

1. **Affichage du formulaire** : L'étudiant demande le formulaire d'évaluation
2. **Récupération des questions** : Le système charge les questions depuis la base de données
3. **Remplissage** : L'étudiant remplit toutes les questions obligatoires et peut ajouter des commentaires
4. **Validation** : Le contrôleur valide la complétude des réponses
5. **Anonymisation** : Le service d'anonymat garantit la confidentialité
6. **Sauvegarde** : Les données sont enregistrées dans une transaction
7. **Notification** : Une confirmation est envoyée à l'étudiant

### Alternatives implémentées

#### Alternative 1 : Évaluation incomplète

- **Déclencheur :** L'étudiant tente de soumettre sans remplir toutes les questions obligatoires
- **Traitement :** Le contrôleur détecte les champs manquants et retourne une erreur de validation
- **Résolution :** L'interface surligne les champs manquants et l'étudiant peut les compléter

#### Alternative 2 : Sauvegarde en brouillon (compatibilité mobile)

- **Déclencheur :** L'étudiant utilise l'application mobile et souhaite reprendre plus tard
- **Traitement :** Le système sauvegarde un brouillon avec les réponses partielles
- **Résolution :** L'étudiant peut reprendre l'évaluation ultérieurement avec ses réponses restaurées

#### Alternative 3 : Erreur système lors de la soumission

- **Déclencheur :** Erreur de connexion ou timeout de la base de données
- **Traitement :** Transaction rollback automatique pour garantir l'intégrité des données
- **Résolution :** Le système conserve les réponses et propose une retentative automatique

### Composants MVC détaillés

#### Vue (Présentation)

- **PageEvaluation** : Interface web principale
- **FormulaireMobile** : Interface mobile responsive

#### Contrôleur (Métier)

- **EvaluationController** : Orchestration du processus d'évaluation
- **AnonymatService** : Garantie de l'anonymat des étudiants
- **NotificationService** : Gestion des notifications

#### Modèle (Données)

- **EvaluationModel** : Gestion des évaluations
- **QuestionModel** : Gestion des questions
- **ReponsesModel** : Gestion des réponses et brouillons

### Aspects techniques importants

1. **Gestion de l'anonymat** : Suppression des métadonnées identifiantes avant sauvegarde
2. **Transactions** : Utilisation de BEGIN/COMMIT/ROLLBACK pour garantir l'intégrité
3. **Compatibilité mobile** : Sauvegarde progressive et restauration de brouillons
4. **Validation** : Vérification côté serveur de la complétude des données

---

## 📈 UC6 - Visualiser le tableau de bord interactif

### Diagramme de séquence

**Fichier :** [Diagramme_Sequence_UC6_Tableau_Bord.puml](Diagramme_Sequence_UC6_Tableau_Bord.puml)

### Scénario idéal

**Description :** L'enseignant ou l'administrateur accède au tableau de bord et visualise ses statistiques d'évaluation avec graphiques interactifs.

**Étapes principales :**

1. **Vérification des permissions** : Le système vérifie le rôle de l'utilisateur
2. **Récupération des évaluations** : Chargement de toutes les évaluations pertinentes
3. **Calcul des statistiques** : Agrégation des données (moyennes, indicateurs)
4. **Analyse de l'évolution** : Calcul des tendances temporelles
5. **Récupération des commentaires** : Affichage des derniers commentaires anonymes
6. **Affichage progressif** : Affichage des KPI, graphiques d'évolution, et répartition par catégories

### Alternatives implémentées

#### Alternative 1 : Aucune donnée disponible

- **Déclencheur :** Enseignant n'ayant pas encore reçu d'évaluations
- **Traitement :** Le contrôleur détecte l'absence de données
- **Résolution :** Affichage d'un message d'accueil encourageant

#### Alternative 2 : Accès mobile avec chargement progressif

- **Déclencheur :** Accès depuis un appareil mobile avec connexion limitée
- **Traitement :** Chargement en mode léger avec données résumées
- **Résolution :** Possibilité de charger les détails complets à la demande

#### Alternative 3 : Comparaison avec moyennes départementales

- **Déclencheur :** L'utilisateur souhaite se comparer à ses pairs
- **Traitement :** Calcul des moyennes globales et du positionnement (quartile, percentile)
- **Résolution :** Affichage de graphiques comparatifs

#### Alternative 4 : Erreur de chargement

- **Déclencheur :** Timeout ou surcharge de la base de données
- **Traitement :** Gestion de l'erreur avec message explicite
- **Résolution :** Bouton de retentative automatique

### Composants MVC détaillés

#### Vue (Présentation)

- **TableauBord** : Interface principale du dashboard
- **GraphiquesInteractifs** : Composants de visualisation (charts.js, D3.js)
- **VueMobile** : Version responsive optimisée

#### Contrôleur (Métier)

- **TableauBordController** : Orchestration du chargement des données
- **StatistiquesService** : Calcul des indicateurs et moyennes
- **EvolutionService** : Analyse des tendances temporelles
- **FiltreService** : Gestion des filtres et tri des données

#### Modèle (Données)

- **EvaluationModel** : Récupération des évaluations
- **StatistiquesModel** : Calculs statistiques et agrégations
- **CommentairesModel** : Gestion des commentaires anonymes

### Aspects techniques importants

1. **Performance** : Calculs optimisés avec agrégations SQL (GROUP BY, AVG)
2. **Interactivité** : Filtrage dynamique sans rechargement complet de la page
3. **Responsive Design** : Adaptation automatique aux différents écrans
4. **Chargement progressif** : Affichage des KPI en priorité, puis graphiques détaillés
5. **Gestion des permissions** : Accès différencié selon le rôle (enseignant vs administrateur)

---

## 🔄 Interactions entre les cas d'utilisation

```
UC1 (Remplir évaluation)
         │
         ├─► Crée des données d'évaluation
         │
         ▼
    Base de données
         │
         ├─► Alimente les statistiques
         │
         ▼
UC6 (Tableau de bord)
```

Les deux cas d'utilisation sont intimement liés :

- **UC1** génère les données brutes (évaluations, réponses, commentaires)
- **UC6** exploite ces données pour produire des visualisations et analyses

---

## 🎯 Points clés de l'architecture MVC

### Séparation des préoccupations

- **Vue** : Uniquement l'affichage, pas de logique métier
- **Contrôleur** : Orchestration et logique métier, pas d'accès direct à la BDD
- **Modèle** : Accès aux données uniquement, pas de logique d'affichage

### Avantages de cette architecture

1. **Maintenabilité** : Modifications indépendantes de chaque couche
2. **Testabilité** : Tests unitaires faciles sur chaque composant
3. **Réutilisabilité** : Services et modèles réutilisables
4. **Scalabilité** : Facile d'ajouter de nouveaux composants

### Services transversaux

- **AnonymatService** : Utilisé dans UC1 pour protéger l'identité
- **StatistiquesService** : Utilisé dans UC6 pour les calculs
- **NotificationService** : Notifications dans plusieurs cas d'utilisation

---

## 📝 Conformité aux exigences

### ✅ Démarche MVC appliquée

- Architecture en trois couches clairement définie
- Séparation des responsabilités respectée
- Services métier identifiés et documentés

### ✅ Scénario idéal détaillé

- Flux complet de A à Z pour chaque cas d'utilisation
- Interactions entre composants clairement définies
- Transactions et persistance des données

### ✅ Alternatives multiples

- **UC1** : 3 alternatives (incomplète, brouillon, erreur système)
- **UC6** : 4 alternatives (pas de données, mobile, comparaison, erreur)
- Gestion des cas d'erreur et chemins alternatifs

### ✅ Hors authentification

- Les deux cas d'utilisation choisis ne concernent pas l'authentification
- Focus sur les fonctionnalités métier principales du système

---

## 🚀 Pour aller plus loin

### Améliorations possibles

1. **Cache** : Mise en cache des statistiques pour améliorer les performances
2. **WebSockets** : Mise à jour en temps réel du tableau de bord
3. **Export** : Génération de rapports PDF/Excel depuis le tableau de bord
4. **IA/ML** : Analyse de sentiment sur les commentaires anonymes

### Tests recommandés

1. **Tests unitaires** : Sur chaque service (Anonymat, Statistiques, etc.)
2. **Tests d'intégration** : Sur les flux complets (UC1, UC6)
3. **Tests de charge** : Simulation de 1000+ étudiants remplissant une évaluation
4. **Tests UI** : Compatibilité navigateurs et mobile

---

**Auteur :** Analyse réalisée dans le cadre du Projet SI  
**Date :** 21 décembre 2025  
**Version :** 1.0
