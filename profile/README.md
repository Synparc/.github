<div align="center">

<img src="https://raw.githubusercontent.com/Synparc/synparc-internal/refs/heads/main/assets/logo.png" alt="Synparc Logo" width="100" />

# Synparc

### Supervision intelligente de parc informatique

**Croisez vos données Active Directory, Microsoft 365 et vos postes en temps réel.**  
Synparc n'est pas un simple outil de monitoring — c'est un moteur de corrélation qui unifie vos sources IT en une seule vue d'ensemble.

[![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE)
[![Status](https://img.shields.io/badge/status-En%20développement-orange?style=flat-square)]()
[![Stack](https://img.shields.io/badge/stack-Node.js%20%7C%20Go%20%7C%20Next.js%20%7C%20PostgreSQL-informational?style=flat-square)]()

</div>

---

## Pourquoi Synparc ?

Les outils de monitoring classiques vous disent *que* quelque chose se passe.  
Synparc vous dit *qui*, *où*, *avec quels droits* — et *si c'est normal*.

| Question | Ce que Synparc sait répondre |
|----------|------------------------------|
| 🖥️ Qui est connecté sur ce poste ? | Session active croisée avec l'AD en temps réel |
| 🔑 A-t-il accès à ce partage réseau ? | Permissions effectives calculées (directes + héritées) |
| ☁️ Possède-t-il une licence M365 adaptée ? | Croisement AD ↔ Microsoft 365 Graph API |
| 📊 Comment se porte ce serveur depuis 48h ? | CPU / RAM / Disque — historique TimescaleDB |

---

## Architecture

Synparc est organisé en **polyrepo modulaire** — chaque composant est indépendant et déployable séparément.

```
                    ┌─────────────────┐
  Active Directory ─►                 │
  Microsoft 365   ─►  synparc-server  ◄─── synparc-web (dashboard)
  Partages SMB    ─►  (Node.js / TS)  │
                    │                 │
  Postes/Serveurs ─►  synparc-agent   │
  (Go · REST/1min)  └────────┬────────┘
                             │
                    ┌────────▼────────┐
                    │   PostgreSQL    │
                    │ + TimescaleDB   │
                    └─────────────────┘
```

---

## Dépôts

| Dépôt | Rôle | Stack |
|-------|------|-------|
| [synparc-server](https://github.com/Synparc/synparc-server) | Backend central — API REST, moteur de corrélation, migrations DB | Node.js / TypeScript |
| [synparc-web](https://github.com/Synparc/synparc-web) | Dashboard — fiches utilisateurs, métriques, explorateur de permissions | Next.js / React |
| [synparc-agent](https://github.com/Synparc/synparc-agent) | Agent léger déployé sur les postes et serveurs | Go / Rust |
| [synparc-connectors](https://github.com/Synparc/synparc-connectors) | Modules de synchronisation AD (LDAP), M365 (Graph API), SMB | Node.js / TypeScript |
| [synparc-installer](https://github.com/Synparc/synparc-installer) | Scripts de déploiement multi-rôles et auto-update | PowerShell |

---

## Stack technique

<div align="center">

![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![Go](https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![TimescaleDB](https://img.shields.io/badge/TimescaleDB-FDB515?style=for-the-badge&logo=timescale&logoColor=black)
![PowerShell](https://img.shields.io/badge/PowerShell-5391FE?style=for-the-badge&logo=powershell&logoColor=white)

</div>

---

## Fonctionnalités v1

- ✅ **Inventaire Active Directory** — utilisateurs, groupes, comptes inactifs, dernières connexions
- ✅ **Sessions actives** — qui est connecté sur quel poste, en temps réel
- ✅ **Permissions effectives** — droits directs + hérités par groupe, avec traçabilité de l'origine
- ✅ **Scan SMB incrémental** — ACLs sur les partages réseau (seuls les dossiers modifiés sont re-scannés)
- ✅ **Intégration Microsoft 365** — licences, MFA, permissions SharePoint via Graph API
- ✅ **Métriques machines** — CPU, RAM, disques avec historique temporel (TimescaleDB)
- ✅ **Déploiement on-premise** — tout tourne chez le client, pas de cloud central
- ✅ **Licensing** — système de clés de licence limitant le nombre de nœuds surveillés

---

<div align="center">

*Synparc est en cours de développement actif.*  
**Syn** (grec : *ensemble, synchronisé*) + **Parc** (parc informatique)

</div>
