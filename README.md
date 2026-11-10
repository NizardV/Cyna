# Cyna

Plateforme SaaS e-commerce de services de cybersécurité, développée en équipe au **DIIAGE (Sup de Vinci)**.
Les clients y parcourent un catalogue de solutions (SOC, EDR, XDR…), s'abonnent et paient en ligne ;
les administrateurs gèrent le catalogue, le contenu et les commandes depuis un back-office.

🌐 **Démo :** https://cyna.nizard.dev

## Dépôts

| Dépôt | Rôle | Stack |
| --- | --- | --- |
| [cyna-web](https://github.com/NizardV/cyna-web) | Site client et back-office | React, TypeScript, Vite, Tailwind CSS, shadcn/ui |
| [cyna-api](https://github.com/NizardV/cyna-api) | API REST | ASP.NET Core (.NET 10), Entity Framework Core, PostgreSQL, Stripe |
| [cyna-app](https://github.com/NizardV/cyna-app) | Application Android | Kotlin, Jetpack Compose (Clean Architecture, MVI), Ktor, Koin |
| cyna-infra *(privé)* | Infrastructure | Docker Compose, Nginx, PostgreSQL, sauvegardes |
| [cyna-autre](https://github.com/NizardV/cyna-autre) *(archivé)* | Documents annexes | Diagramme de la base de données |

## Architecture

```
            ┌──────────────┐        ┌──────────────┐
 Navigateur │   cyna-web   │  HTTPS │   cyna-api   │──── Stripe (paiement)
 ──────────►│  SPA (Nginx) │───────►│ ASP.NET Core │──── Resend (e-mails)
            └──────────────┘        └──────┬───────┘
 Android    ┌──────────────┐               │
 ──────────►│   cyna-app   │───────────────┤
            └──────────────┘        ┌──────┴───────┐
                                    │  PostgreSQL  │
                                    └──────────────┘
```

Les images Docker de cyna-web et cyna-api sont construites par GitHub Actions et déployées sur un VPS OVH,
derrière Nginx avec SSL : la branche `dev` alimente le **staging**, la branche `main` la **production**.
