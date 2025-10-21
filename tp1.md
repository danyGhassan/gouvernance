
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

# Atelier 3 – Scénarios stratégiques

## Cartographie simple de l'écosystème


L’écosystème de DataSecuRetail repose sur plusieurs acteurs interconnectés :

- **Hébergeur cloud** : héberge le site web marchand et la base de données clients. Il dispose d’accès administratifs à l’infrastructure.
- **Prestataire IT** : chargé de la maintenance et du support technique, avec accès à distance (VPN ou SSH).
- **Plateforme de paiement tierce** : gère les transactions bancaires et envoie des confirmations de paiement via API ou webhooks.
- **Transporteur logistique** : reçoit automatiquement les commandes validées et transmet les informations d’expédition.
- **Clients** : accèdent au site web pour consulter, commander et payer des produits.
- **DataSecuRetail (système interne)** : site web, mini-ERP, traitement des commandes, mise à jour des données clients.

Chaque acteur échange des données ou des accès avec DataSecuRetail, formant un réseau de confiance exposé aux risques indirects.

## 2. Scénario stratégique 1 (fonctionnel)

- **Source de risque** : fournisseur tiers compromis (hébergeur cloud)  
- **Voie d’attaque** : l’attaquant exploite une vulnérabilité non corrigée dans l’infrastructure de l’hébergeur et accède directement aux serveurs du site. Il chiffre la base de données et rend le site indisponible.  
- **Valeur métier touchée** : disponibilité du site web et intégrité des données clients  
- **Événement redouté réalisé** : interruption totale du service e-commerce et corruption/chiffrement des données critiques.  
- **Gravité estimée** : 4 (réf. Atelier 1)

## 3. Scénario stratégique 2 (fonctionnel)

- **Source de risque** : compromission d’un employé interne (phishing ou mot de passe faible)  
- **Voie d’attaque** : l’attaquant vole les identifiants d’administration et modifie les informations de paiement ou exfiltre les données clients via le mini-ERP ou la console de paiement.  
- **Valeur métier touchée** : sécurité des paiements et confidentialité des données clients  
- **Événement redouté réalisé** : fraude financière + fuite massive de données personnelles (RGPD).  
- **Gravité estimée** : 4 (réf. Atelier 1)

# Atelier 4 – Scénarios opérationnels

**Scénario choisi (sélection)**  
Nous retenons le scénario stratégique 2 : **compromission d’un employé interne (phishing / mot de passe faible)** conduisant à fraude sur les paiements et exfiltration de données clients. Ce scénario est à la fois critique (impact financier et RGPD) et vraisemblable compte tenu des contrôles actuels.

## Déroulé opérationnel — étapes (6 à 8 étapes claires)

1. **Reconnaissance ciblée** — L'attaquant collecte des informations publiques sur DataSecuRetail et ses employés (LinkedIn, pages “contact”, répertoire) pour identifier une cible interne (ex. comptabilité, support, admin ERP).  
   *Composant visé : sources publiques / comptes mail ciblés.*

2. **Envoi de phishing** — L'attaquant envoie un e-mail de phishing soigneusement rédigé (faux message client, facture, ou alerte de paiement) contenant un lien vers une page de credential-harvesting ou une pièce jointe malveillante.  
   *Composant visé : boîte mail de l'employé, client de messagerie.*

3. **Compromission des identifiants** — L'employé, sans formation suffisante et utilisant un mot de passe simple, saisit ses identifiants sur la fausse page ou ouvre la pièce jointe qui installe un stealers/backdoor. L'attaquant récupère les identifiants ou obtient un accès initial sur le poste.  
   *Composant visé : poste utilisateur Windows 11 de l'employé, session mail.*

4. **Escalade/usage des accès** — Avec ces identifiants, l'attaquant se connecte à la console du mini-ERP ou à la console d'administration de la plateforme de paiement (selon les droits), ou installe un accès persistant (web shell, reverse shell) sur le poste/serveur compromis.  
   *Composant visé : mini-ERP, console de paiement, serveur applicatif, VPN/SSH si les mêmes identifiants y donnent accès.*

5. **Actions malveillantes sur le SI** — L'attaquant modifie les coordonnées bancaires de certaines commandes, déclenche remboursements frauduleux, ou exporte des enregistrements clients (noms, adresses, emails, éventuellement éléments de paiement).  
   *Composant visé : base de données clients, module commandes du mini-ERP, API paiement.*

6. **Exfiltration des données & dissimulation** — Les données volées sont compressées/chiffrées et exfiltrées via un canal chiffré (HTTPS vers un serveur contrôlé) ; l'attaquant efface ou altère journaux pour retarder la détection.  
   *Composant visé : logs applicatifs, poste compromis, connexion réseau sortante.*

7. **Monétisation / exploitation** — Les fonds détournés sont encaissés via des comptes mule ou vendus sur le marché noir ; les données personnelles sont vendues ou utilisées pour fraudes supplémentaires.  
   *Composant visé : services externes / comptes tiers exploités pour blanchiment.*

8. **Impact et découverte** — L’entreprise détecte anomalies (clients se plaignent, litige payment, ou alertes externes) ; réponse tardive en raison d’une supervision faible et d’alertes non paramétrées.  
   *Composant visé : SI de supervision / helpdesk, services juridiques/commercials.*

## Biens supports impliqués (liste)

- Postes utilisateurs (compte employé cible, client mail)  
- Serveur applicatif / console d'administration du site  
- Mini-ERP (module gestion commandes, interfaces admin)  
- Console/API de la plateforme de paiement (webhooks, tokens)  
- Base de données clients (hébergée chez prestataire cloud)  
- Accès VPN / accès du prestataire IT (si mêmes credentials ou pivot possible)  
- Journaux (logs applicatifs, logs d’accès)  
- Sauvegardes (pour évaluer restauration possible)  
- Connexions réseau sortantes (canal d’exfiltration)

## Évaluation de la vraisemblance

**Cotation : Probable**

**Justification :** l’environnement décrit présente plusieurs facteurs favorisant ce scénario — absence de MFA, mots de passe simples, faible sensibilisation au phishing et supervision quasi inexistante ; ces conditions rendent l’exploitation par phishing et l’usage d’identifiants compromis relativement facile et crédible.

---


# Atelier 5 – Traitement du risque et plan d’action

## 1. Synthèse des risques

| Scénario | Gravité | Vraisemblance | Niveau global |
|----------|----------|---------------|----------------|
| Scénario 1 – Hébergeur compromis → indisponibilité + chiffrement | 4 | Possible | Élevé |
| Scénario 2 – Phishing interne → fraude + fuite de données | 4 | Probable | Critique |

**Échelle utilisée :**  
- **Faible** = impact et proba faibles  
- **Modéré** = impact moyen OU proba modérée  
- **Élevé** = impact fort OU proba forte  
- **Critique** = impact et proba très forts (impact légal + financier + médiatique)

## 2. Traitement des risques

| Scénario | Stratégie de traitement | Justification |
|----------|--------------------------|----------------|
| Scénario 1 – Hébergeur compromis | Réduire | Limiter l’impact et améliorer la continuité (sauvegardes, PRA). |
| Scénario 2 – Phishing interne | Réduire | C’est un risque critique mais maîtrisable (MFA + détection). |

*Aucun risque n’est transféré ou évité ici — le cœur du business repose sur ces fonctions.*

## 3. Plan d’action priorisé

| Mesure | Objectif | Responsable | Délai |
|--------|----------|-------------|--------|
| **Mise en place MFA / 2FA** sur comptes admin + prestataire | Réduire probabilité (compromission identifiants) | DSI + Prestataire IT | Court terme |
| **Sensibilisation anti-phishing + simulation interne** | Réduire probabilité (erreur humaine) | Direction + RH | Court terme |
| **Supervision + alertes en temps réel SI critique** | Réduire probabilité et impact (détection précoce) | DSI | Court terme |
| **Tests réguliers de restauration + renforcement sauvegardes** | Réduire impact (résilience) | DSI | Moyen terme |
| **Segmentation / limitation des privilèges par profil** | Réduire impact (limiter mouvement latéral) | Prestataire IT | Moyen terme |
| **Contrat / exigence de sécurité avec l’hébergeur (SLA, PRA)** | Réduire impact + transférer partiellement | Direction | Moyen à long terme |

---

