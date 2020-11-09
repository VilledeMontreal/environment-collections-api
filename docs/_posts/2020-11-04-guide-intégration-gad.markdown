---
layout: post
title:  "Guide d'intégration pour les sites de déversement"
date:   2020-11-04 14:10:48 -0500
categories: 
--- 
[version PDF](/assets/integration-GAD.pdf)

## Mise en contexte

La Ville de Montréal modernise ses autorisations de déverser pour les matières résiduelles avec le système GAD ( gestion des autorisations de déverser ). Présentement, des billets papier sont utilisés par les différents transporteurs pour accéder et déverser des matières dans les sites de déversement sous contrats avec la Ville de Montréal. 

Le système GAD permet d’abandonner le papier et de passer aux autorisations de déverser électroniques. Ce passage offre plusieurs avantages pour la Ville de Montréal et ses partenaires:
- Gestion allégée du processus de facturation à la Ville.
- Accélération de la vérification des autorisations aux guérites.
- Diminution du risque d’erreurs.
- Réduction du nombre d’autorisations utilisées anormalement.

## Intégration au système GAD

L’utilisation des autorisations électroniques nécessite qu’une intégration soit faite par un programmeur informatique professionnel de votre choix afin de rendre le système de gestion des balances apte à: 

Vérifier qu’un camion, qui se présente à votre guérite, soit autorisé par la Ville de Montréal à déverser des matières dans votre site.
Transmettre les heures de passage et les pesées à l’entrée et à la sortie du camion.

La communication entre votre système et le système GAD de la Ville de Montréal se fait via une API ( application programming interface ou interface de programmation ) sous protocole de communication sécurisé HTTPS et format de données JSON.  

Le diagramme ci-dessous représente les interactions avec le système GAD.

![interractions](/assets/interractions.png)

## Spécification de l’API 

La spécification de l’API pour communiquer avec le système GAD est disponible à l’emplacement suivant: https://api.montreal.ca/documentation/environment/collections/v1/specification. 

Veuillez utiliser l’éditeur Open API de votre choix, par exemple https://editor.swagger.io/, pour lire la spécification. Une version pdf de la spécification API est également disponible en annexe. 

## Support GAD

Pour toutes questions concernant l’intégration au système GAD, veuillez svp écrire à l’adresse support.gad@montreal.ca.

## Clés API 

La communication avec le système GAD nécessite une clé API pour s’authentifier. Le contenu des clés et la manière de les obtenir diffèrent selon l’environnement informatique : 

Environnement d’acceptation : Veuillez svp écrire un courriel à l’adresse support.gad@montreal.ca pour demander la clé en mentionnant le site de déversement concerné. 

Environnement de production : La clé API de l’environnement de production vous sera fournie par l’équipe du support informatique GAD de la Ville de Montréal une fois les tests d’acceptation réussis.

## Indisponibilité de GAD

Si le système GAD devenait indisponible, pour quelque motif que ce soit, le système de gestion de balance du site doit être en mesure de respecter le processus suivant qui sera déclenché

Le Service de l’environnement de la Ville de Montréal contactera le responsable du site afin de lui demander de passer en mode manuel.

Si un ou plusieurs camions disposent d’une autorisation de déverser électronique obtenue avant l’indisponibilité de GAD 

La Ville de Montréal enverra par courriel au responsable de site de déversement un fichier en format csv contenant les informations suivantes: numéro d’immatriculation, numéro de camion, compagnie de transport, territoire de collecte et matière collectée. 

Les camions inscrits sur cette liste devront pouvoir accéder le site sans autorisation de déverser papier.

Pour chaque camion de cette liste, le site remplira le fichier csv manuellement avec les quatre informations suivantes : poids du camion avant le déversement, heure de la pesée  avant le déversement, poids du camion après le déversement, heure de la pesée après le déversement.

La Ville de Montréal s'assurera d’entrer les données dans le système GAD à posteriori. 

Pour les camions n’ayant pas été autorisés avant l’indisponibilité de GAD 

Ces camions ne figurent donc pas sur la liste transmise par la Ville de Montréal par courriel en format csv

Chaque camion dans cette situation devra être muni d’une autorisation papier afin d’accéder au site sans quoi il devra être refusé car ce déversement ne pourra être facturé à la Ville de Montréal.

Durant toute la durée de l'indisponibilité de GAD, les billets d’autorisation papier doivent être envoyés avec la facture au Service de l’environnement de la Ville de Montréal.

Lorsque la situation sera rétablie et que GAD sera de nouveau disponible, la Ville de Montréal contactera le responsable site de déversement afin de l’aviser du retour aux autorisations électroniques. À partir de ce moment, plus aucun billet d’autorisation papier ne devra être accepté par le site

Tests d’acceptation 

La Ville de Montréal réalise des tests d’acceptation, afin de s’assurer que le système de gestion de balance est intégré correctement au système GAD avant que le site de déversement puisse utiliser les autorisations de déverser électroniques en production.

Ces tests seront réalisés dans votre environnement d’acceptation. Cet environnement doit être indépendant de celui utilisé en production. L’environnement d’acceptation doit permettre de simuler les interactions avec les différentes composantes matérielles (balances, bornes avec keypad, caméra, etc.) sans dépendre du déploiement physique du système de gestion des balances.

Les scénarios de tests seront disponibles sous peu. La personne responsable d’intégrer le système de gestion de balance au système GAD doit en prendre connaissance avant de débuter son travail. Une fois les travaux d’intégration du site au système GAD terminés, elle est responsable de vérifier elle-même l’ensemble des scénarios de tests avant de contacter la Ville de Montréal via support.gad@montreal.ca pour l’acceptation officielle.

Dans la mesure du possible, il est préférable que la Ville de Montréal réalise les tests d’acceptation de manière autonome, à distance, dans votre environnement d’acceptation en jouant le rôle du site de déversement. 
