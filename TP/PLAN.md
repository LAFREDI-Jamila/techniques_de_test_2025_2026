# PLAN - Techniques de Test

## 1. Introduction

Le but de ce TP n’est pas de faire une grosse application,  
mais surtout d’apprendre à **tester correctement un programme**.

Le programme à faire s’appelle **Triangulator**.  
C’est un petit service web (micro-service) qui reçoit un ensemble de points 2D,  
fait des calculs pour former des triangles, puis renvoie le résultat.  

L’objectif principal du TP, c’est surtout de mettre en place **différents types de tests**  
pour vérifier le bon fonctionnement du code.  

Dans l’architecture, on a :
- **PointSetManager** : gère les ensembles de points (il les stocke et les renvoie),
- **Database** : sert à enregistrer les points,
- **Triangulator** : c’est la partie que je dois faire, qui calcule la triangulation,
- **Client** : c’est celui qui envoie les requêtes et reçoit la réponse.

---

## 2. Organisation du travail

Je vais faire le projet en plusieurs étapes :

### Étape 1 – Séance 1
- Lire et comprendre le sujet (fait).  
- Rédiger ce plan pour expliquer comment je vais m’organiser.  
- Créer les dossiers de base du projet :  
  `triangulator/` pour le code,  
  `tests/` pour les tests.  

### Étape 2 – Prochaines séances
- Mettre en place les outils : `pytest`, `coverage`, `ruff`, `pdoc3`.  
- Faire le `Makefile` avec les commandes pour lancer les tests, vérifier le code, etc.  
- Commencer à écrire les tests même si le code n’est pas encore complet (approche "test first").  

### Étape 3 – Dernière séance
- Finir l’implémentation du Triangulator.  
- Vérifier que tous les tests passent.  
- Générer la doc avec `pdoc3`.  
- Faire le fichier `RETEX.md` pour le retour d’expérience.

---

## 3. Fonctionnement du Triangulator

Le Triangulator sert à créer des **triangles à partir d’un ensemble de points**.  
Il reçoit un identifiant (`pointSetId`), récupère les points depuis le **PointSetManager**,  
puis calcule les triangles et les renvoie au client.  

Le résultat est envoyé en **format binaire**, qui contient :
- la liste des points (X et Y),  
- puis la liste des triangles (avec les indices des points).  

Je ne vais pas faire un vrai algorithme compliqué,  
le but est surtout de **simuler le fonctionnement** et de **tester tout le comportement**.

---

## 4. Données et tests prévus

Les échanges entre les services se font en **binaire** :
- Pour un `PointSet` :  
  4 octets → nombre de points,  
  puis 8 octets par point (4 pour X, 4 pour Y).  
- Pour un `Triangles` :  
  même chose pour les points, puis une partie avec les triangles et leurs indices.

### Tests que je prévois
- Vérifier qu’un `PointSet` avec 3 points donne bien 1 triangle.  
- Vérifier qu’un `PointSet` vide ne provoque pas d’erreur.  
- Tester les cas particuliers (points doublés, points alignés).  
- Vérifier les erreurs de format (fichier mal formé, tailles incorrectes).  
- Vérifier que la réponse est bien renvoyée au bon format.

---

## 5. Types de tests

- **Tests unitaires** : pour tester les fonctions internes (conversion binaire, calculs simples, etc.).  
- **Tests d’API** : pour vérifier la route `/triangulation/{pointSetId}` (statuts 200, 400, 404...).  
- **Tests de performance** : mesurer le temps de calcul avec beaucoup de points.  
- **Tests de robustesse** : voir si le service gère bien les mauvaises données.

---

## 6. Outils utilisés

- `pytest` pour exécuter les tests  
- `coverage` pour la couverture de code  
- `ruff` pour vérifier la qualité du code  
- `pdoc3` pour la documentation  
- `make` pour automatiser les commandes (tests, doc, etc.)

---

## 7. Objectif final

Avoir un petit projet clair et bien organisé,  
avec des tests pertinents qui couvrent les différents cas possibles.  

Le but est de montrer que j’ai compris comment **organiser et tester un programme proprement**,  
et pas juste écrire du code qui “marche”.

