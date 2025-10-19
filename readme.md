# TP 0 – Introduction à Jakarta EE
**Étudiant** : Oussama Essalmani  
**Groupe** : G1  
**Numéro** : 9

---

## Description
Ce projet est le TP 0 du cours “Introduction à Jakarta EE” (CDI + JSF + Maven + Payara).  
L’application permet à un utilisateur de saisir une question, de choisir un rôle pour l’API, puis d’afficher un résultat issu d’un traitement personnalisé.

---

## Fonctionnalités implémentées
- Interface utilisateur en JSF (page `index.xhtml`).
- Backing bean CDI (classe `Bb`) en portee *view*.
- Traitement personnalisé dans la méthode `envoyer()` :
    - Calcul du **nombre de caractères** de la question.
    - Calcul du **nombre de voyelles** (y compris accents : à â ä é è ê ë î ï ô ö ù û ü).
    - Calcul du **nombre de mots** dans la question.
    - Affichage des résultats dans la zone de réponse et historique de conversation.

---

## Usage
1. Ouvrir le projet dans IntelliJ IDEA Ultimate.
2. Importer avec Maven, recharger les dépendances.
3. Configurer le serveur d’application : Payara Server 6 (version 6.2025.9).
4. Exécuter la configuration de déploiement.
5. Naviguer vers `http://localhost:8080/EMSI_IA_G1_TP0_9/` (ou l’URL indiquée) dans un navigateur.
6. Saisir une question, sélectionner un rôle, puis cliquer sur **Envoyer**.
7. En cas d’erreur (champ question vide), un message est affiché.

---

## Explication des messages d’erreur
- **“Il manque le texte de la question”** :  
  Dans le bean `Bb`, la condition `if (question == null || question.isBlank())` détecte que l’utilisateur n’a pas saisi de texte. Le bean crée alors un `FacesMessage` de sévérité `ERROR` via `facesContext.addMessage(...)`.
- **“Vous devez indiquer le rôle de l’API”** :  
  Dans la page JSF, la balise `<p:selectOneMenu … required="true" requiredMessage="Vous devez indiquer le rôle de l'API">` impose que l’utilisateur choisisse un rôle. Le message est affiché automatiquement lorsque ce champ est laissé vide.

---

## Rôle de l’API
Le backing bean gère un rôle système (`roleSysteme`) choisi par l’utilisateur parmi :
- Assistant (helpful assistant)
- Traducteur anglais-français
- Guide touristique  
  L’API est simulée ici : elle n’appelle pas de LLM réel, mais le rôle est conservé pour préparer les prochains TPs et montrer l’architecture.

---

## Structure du projet
- `src/main/java/ma/emsi/essalmani/tp0_essalmani/jsf/Bb.java` – Backing bean CDI.
- `src/main/webapp/index.xhtml` – Interface utilisateur JSF.
- `pom.xml` – Configuration Maven (Jakarta EE Web Profile + PrimeFaces).
- `web.xml` – Fichier de configuration minimal, bienvenue page.
- Fichiers de ressources éventuels (CSS, JS) sous `src/main/webapp/resources/`.

---

## Bonus implémenté
Traitement personnalisé pour ce TP 0 : calcul du nombre de caractères, du nombre de voyelles et du nombre de mots dans la question.  
Ce traitement est simple mais montre que l’application répond bien aux attentes et que le mécanisme JSF/CDI fonctionne.

---

## Contact
Pour toute question ou remarque : Oussama Essalmani – essalmanioussama@gmail.com
