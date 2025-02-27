---
title: "Passer d'une facturation à l'heure à mensuelle"
excerpt: 'Découvrez comment modifier le type de facturation de votre instance Public Cloud'
slug: changer-type-facturation-public-cloud
section: 'Gestion de projets'
order: 5
---

**Dernière mise à jour le 10/09/2021**

## Objectif

Lors de la création d’une instance Public Cloud, vous pouvez choisir entre une facturation à l’heure ou une facturation mensuelle. Les instances « à l'heure » sont facturées en *pay-as-you-go* , c'est-à-dire que chaque utilisateur paie en fin de mois, pour chaque heure commencée, la somme des ressources réellement consommées.
<br>Les instances assujetties à un taux mensuel sont 50 % moins chères que les instances assujetties à un taux horaire pour la même durée. Chaque mois entamé est facturé en fin de mois.
<br>Si vous avez initialement choisi une facturation à l'heure, vous pouvez passer à la facturation mensuelle à tout moment.

**Ce guide explique comment passer d'une facturation à l'heure vers une facturation mensuelle.**

> [!warning]
>
> Le passage d'une facturation mensuelle vers une facturation à l'heure n'est pas possible. Si vous voulez passer à la facturation à l'heure, il vous faudra supprimer l’instance facturée mensuellement, puis créer une nouvelle instance et choisir la facturation à l'heure. Dans ce cas, nous vous conseillons de suivre ces étapes :
>
>- Créez un <i>snapshot </i>de votre instance actuelle ;
>
>- Créez une nouvelle instance à partir de ce <i>snapshot </i>;
>
>- Supprimez l’instance à facturation mensuelle.
>

## Prérequis

- Vous devez avoir créé une [instance Public Cloud](https://www.ovh.com/ca/fr/public-cloud/){.external}.
- Vous devez être connecté à votre [espace client OVHcloud](https://ca.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/ca/fr/&ovhSubsidiary=qc){.external}.

## En pratique

Dans [votre espace client](https://ca.ovh.com/auth/?action=alleraugestionnaire){.external}, cliquez sur `Public cloud`{.action}, choisissez le projet Public cloud concerné puis cliquez sur `Instances`{.action} dans le menu `Compute`. Cliquez sur le bouton `...`{.action} à droite de l'instance pour laquelle vous souhaitez modifier la facturation. Vous verrez alors le bouton `Passer au forfait mensuel`{.action} :

![Modifier le mode de calcul des factures](images/switch_to_monthly_updated.png){.thumbnail}

Il vous faudra ensuite confirmer que vous souhaitez modifier le mode de facturation :

![Confirmer la modification du mode de calcul des factures](images/confirm_to_monthly_updated.png){.thumbnail}

Après validation de votre choix, vous recevrez immédiatement une facture mensuelle au prorata. La prochaine facture inclura la partie du mois à l'heure (le 1er du mois jusqu'au changement) et les nouveaux frais mensuels.

## Aller plus loin

Échangez avec notre communauté d'utilisateurs sur <https://community.ovh.com>.
