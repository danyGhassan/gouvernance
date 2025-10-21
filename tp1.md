
# Atelier 1 – Cadrage et socle de sécurité

## Périmètre de l’étude

L’analyse porte sur la chaîne e-commerce de DataSecuRetail, incluant le site web marchand, la base de données clients hébergée chez le prestataire cloud, la plateforme de paiement tierce, ainsi que l’intégration avec le transporteur logistique. Les systèmes internes comme le serveur de fichiers et les postes utilisateurs sont considérés indirectement dans la mesure où ils influencent la continuité de la vente en ligne.

## Mission principale et processus critiques

DataSecuRetail vend des objets technologiques via son site web. La mission principale est de permettre aux clients de passer et recevoir leurs commandes de manière sécurisée et fiable. Les processus critiques incluent :

- Gestion des commandes via le mini-ERP
- Traitement des paiements en ligne
- Transmission des commandes au transporteur
- Mise à jour et protection des données clients

## Tableau valeurs métier / événements redoutés / gravité

| Valeur métier | Événement redouté | Gravité (1–4) | Justification |
|---------------|------------------|---------------|---------------|
| Disponibilité du site web | Site indisponible plusieurs heures | 4 | Perte directe de ventes, impact sur la réputation et confiance clients |
| Intégrité des données clients | Altération ou corruption de la base clients | 4 | Risque de commandes erronées, fraude possible, obligation légale RGPD |
| Sécurité des paiements | Vol ou fraude des transactions | 4 | Impact financier direct et juridique, perte de confiance client |
| Fiabilité de la chaîne logistique | Commandes mal transmises ou retardées | 3 | Insatisfaction client, perte potentielle de chiffre d’affaires |
| Confidentialité des informations clients | Divulgation de données personnelles | 4 | Impact légal (RGPD), réputationnel et commercial majeur |

## Exigences de sécurité recommandées

- Authentification forte (MFA/2FA) pour tous les accès critiques.
- Sauvegardes régulières et tests de restauration fréquents.
- Chiffrement des données sensibles au repos et en transit.
- Supervision et alertes en temps réel sur les services critiques.
- Sensibilisation des employés aux risques de phishing et bonnes pratiques.

## Mise en œuvre actuelle (observations / écarts)

- Authentification limitée à des mots de passe simples, pas de 2FA.
- Sauvegardes hebdomadaires seulement, sans test régulier de restauration.
- Données sensibles stockées sur le cloud, mais chiffrement partiel ou absent.
- Supervision quasi inexistante, alertes non paramétrées.
- Sensibilisation à la cybersécurité faible, risques liés aux emails malveillants non couverts.




# Atelier 2 – Identification des sources de risque

## Objectif
Comprendre qui pourrait menacer l’entreprise et pour quelles raisons.

## Tableau sources de risque / objectifs / capacités et motivation

| Source de risque | Type | Objectifs visés | Motivation | Ressources | Activité |
|-----------------|------|-----------------|------------|------------|----------|
| Employé interne négligent | Interne | Accidentellement compromettre la confidentialité ou la disponibilité (ex. : suppression de données, mauvaise manipulation) | Moyenne | Accès au SI interne, connaissances limitées | Souvent |
| Administrateur IT externe | Interne/Externe | Mauvaise configuration ou erreur technique pouvant provoquer indisponibilité ou fuite de données | Faible à moyenne | Accès administratif, compétences techniques | Occasionnel |
| Cybercriminel | Externe | Vol de données clients, fraude financière via paiements compromis | Élevée | Compétences techniques, outils hacking, ressources financières | Souvent |
| Hacktiviste | Externe | Dénoncer l’entreprise, dégrader sa réputation, ex. via défacement du site | Moyenne | Compétences techniques limitées à modérées | Occasionnel |
| Concurrent malveillant | Externe | Obtenir des informations commerciales confidentielles ou perturber le service | Moyenne à élevée | Ressources financières et humaines, techniques de renseignement | Occasionnel |
| Fournisseur tiers compromis | Externe | Propager une attaque indirecte sur DataSecuRetail (ex. : hébergeur, paiement, logistique) | Moyenne | Accès aux systèmes interconnectés, compétences techniques | Occasionnel |
| Malware / ransomware automatisé | Externe | Indisponibilité du SI, chantage financier | Élevée | Très automatisé, nécessite peu d’intervention humaine | Fréquent |
