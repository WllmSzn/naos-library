# Bibliothèque de DNA

Les systèmes de design (« Design DNA ») utilisés par [Naos](../Naos). **Ouvrir [index.html](index.html)** pour voir toutes les DNA en un coup d'œil (aperçus, couleurs, polices, modes servis), ou lire [CATALOG.md](CATALOG.md).

## Organisation

Une famille par dossier, une DNA par sous-dossier :

```
artefact/                 ARTEFACT : thèmes produit et déclinaisons marketing
  artefact-dark/
    dna.json              la DNA : identité commune + un bloc par mode
    previews/             aperçus générés (un par mode)
  patterns/
    product-desktop/      sections partagées par les DNA de la famille
inspirations/             DNA tirées de sites de référence (Linear, Better Stack…)
base/                     DNA d'origine de Naos, sans source extérieure
clients/                  une sous-famille par client : clients/<client>/<id>/dna.json
```

- Le dossier d'une DNA porte son `id`.
- Une famille peut avoir des sous-familles (`clients/acme`).
- Une section propre à une seule DNA se range dans `<famille>/<id>/patterns/<mode>/`. Une section partagée par une famille va dans `<famille>/patterns/<mode>/`, avec un champ `"dna"` pour la réserver à certaines DNA.

## Ajouter ou modifier une DNA

- **Avec Claude** (Naos branché) : *« Crée une DNA … dans la famille clients/acme »*. `save_dna` la range au bon endroit. Pour une DNA existante, elle est réécrite à son emplacement.
- **À la main** : copier le dossier d'une DNA proche, renommer le dossier et l'`id`, modifier `dna.json`.

Ensuite, depuis le dossier de Naos, une commande par ligne :

```powershell
cd C:\Users\Artefact\Naos
npm.cmd run audit -- <id>             # rendu de toutes les sections avec la DNA
npm.cmd run catalog -- --previews     # régénère index.html, CATALOG.md et les aperçus
```

Une DNA invalide (contraste insuffisant, champ manquant, dossier mal nommé) n'est pas chargée par Naos. Elle apparaît en rouge en tête de `index.html`.

## Branchement avec Naos

Naos lit cette bibliothèque via `Naos/naos.config.json` :

```json
{ "library": ["C:/Users/Artefact/naos-library"] }
```

On peut y lister plusieurs bibliothèques, par exemple une personnelle et une par client. La variable d'environnement `NAOS_LIBRARY` a priorité sur ce fichier.
