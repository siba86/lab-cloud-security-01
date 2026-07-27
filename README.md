# Lab Cloud Security — Durcissement d'une VM Azure

## Contexte

Projet personnel de montée en compétences en sécurité cloud, réalisé sur un abonnement Azure Free Trial. L'objectif : déployer une machine virtuelle exposée sur Internet, identifier ses faiblesses de sécurité par défaut, puis les corriger — en documentant chaque étape comme un audit réel (constat / recommandation / statut).

## Architecture

- **Abonnement** : Azure Free Trial
- **Groupe de ressources** : `rg-lab-security` (région East US)
- **VM** : `vm-lab-01`, Ubuntu Server 22.04 LTS, Standard_D2s_v7
- **Réseau** : VNet + subnet + NSG créés automatiquement à la création de la VM
- **Accès** : SSH (clé publique/privée), pas de mot de passe

## Ce qui a été fait

| # | Point contrôlé | Constat initial | Action |
|---|---|---|---|
| 1 | Exposition réseau (SSH) | Port 22 ouvert à toute source Internet (Any) | Règle NSG restreinte à l'IP publique de l'administrateur (`/32`) |
| 2 | Authentification du compte | MFA non vérifié sur le compte Microsoft | Vérification en deux étapes activée |
| 3 | Posture de sécurité cloud | Defender for Cloud non activé | Plan gratuit (Foundational CSPM) activé |
| 4 | Maîtrise des coûts | Aucune protection contre une VM oubliée allumée | Alerte de budget (5$/mois) + arrêt automatique programmé (23h Paris) |

Rapport d'audit complet (constat / risque / recommandation / statut) : voir [`RAPPORT_AUDIT_LAB_CLOUD_SECURITY.docx`](./RAPPORT_AUDIT_LAB_CLOUD_SECURITY.docx).

Captures d'écran disponibles dans le dossier [`screenshots/`](./screenshots) :

- `01-nsg-ssh-avant.png` — règle NSG SSH avant durcissement (Source = Tous)
- `02-nsg-ssh-apres.png` — règle NSG SSH après durcissement (Source = IP admin uniquement)
- `03-mfa-active.png` — vérification en deux étapes activée sur le compte
- `04-vm-connexion-ip-masquees.png` — panneau de connexion SSH de la VM (IP masquées)

## Compétences démontrées

- Provisionnement d'infrastructure cloud (VM, réseau, NSG) via le portail Azure
- Durcissement réseau : principe du moindre privilège appliqué à un groupe de sécurité réseau
- Connexion et administration SSH sécurisée par clé
- Activation et lecture des recommandations Microsoft Defender for Cloud (CSPM)
- Gestion des coûts cloud (alertes de budget, arrêt automatique)
- Rédaction de rapport d'audit sécurité (format constat/recommandation/statut)

## Notes

Les adresses IP réelles et informations personnelles ont été anonymisées dans le rapport et les captures avant publication.
