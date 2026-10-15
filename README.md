# TP 1 : Inversion de Contrôle et Réflexion en Java

## Description du travail réalisé
Dans ce projet, j'ai mis en place une application Java illustrant le principe du couplage faible et de l'injection de dépendances, sans utiliser de framework externe comme Spring. 

L'objectif de mon implémentation était de comprendre comment charger des classes et lier des composants dynamiquement à l'exécution en exploitant uniquement l'API de réflexion native de Java (`java.lang.reflect`).

## Architecture et fonctionnement
Pour structurer le projet proprement sous Maven, j'ai organisé le code en trois packages principaux dans `src/main/java` :

* **`dao`** : Contient l'interface `IDao` et son implémentation `DaoImpl` qui simule la récupération d'une donnée.
* **`metier`** : Contient l'interface `IMetier` et la classe `MetierImpl` qui effectue le traitement (calcul) en s'appuyant sur l'interface `IDao`.
* **`presentation`** : Contient la classe `Presentation2` qui joue le rôle de conteneur léger.

Au lieu d'instancier les classes avec l'opérateur `new` (ce qui créerait un couplage fort), j'ai utilisé un fichier `config.txt` contenant le nom complet des classes à charger.

## Ce que j'ai appris et appliqué
* **Chargement dynamique** : Lecture du fichier `config.txt` et utilisation de `Class.forName()` ainsi que `getDeclaredConstructor().newInstance()` pour instancier `DaoImpl` et `MetierImpl` à la volée.
* **Injection par réflexion** : Récupération dynamique de la méthode `setDao` via `getMethod()` et invocation sur l'objet métier avec `invoke()` pour injecter la dépendance.
* **Maintenance facilitée** : Grâce à cette approche, il suffit de modifier une ligne dans `config.txt` pour changer d'implémentation DAO ou Métier sans jamais toucher au code source ni recompiler le projet.

---

## Résultat d'exécution

Lors du lancement de la classe `Presentation2`, le programme lit le fichier de configuration, instancie les deux couches dans l'ordre, réalise l'injection de dépendance, puis appelle la méthode `calcul()`.

Voici la trace d'exécution obtenue dans le terminal d'IntelliJ IDEA qui confirme le chargement dynamique des classes et affiche le résultat final du calcul :

<img width="1861" height="460" alt="image" src="https://github.com/user-attachments/assets/da835335-01e1-4089-bded-308bf7fcfd92" />
