<p align="center">
  <img src="assets/rustine.svg" width="140" alt="Rustine">
</p>

<h1 align="center">Rustine</h1>

<p align="center">
  Le diagnostic gratuit de votre PC Windows, en un seul fichier de moins de 1 Mo.<br>
  Sans installation, sans publicité, sans abonnement.
</p>

<p align="center">
  <a href="https://github.com/samirmedani/rustine/releases/latest/download/Rustine.exe"><b>Télécharger Rustine.exe</b></a>
  &nbsp;·&nbsp;
  <a href="https://yatofix.com/rustine">Page officielle</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/samirmedani/rustine/releases">Toutes les versions</a>
</p>

---

Rustine passe votre PC Windows au crible et vous dit ce qui ne va pas, avec la marche à suivre pour chaque problème. Vous lancez le fichier, vous choisissez une formule, et le rapport s'ouvre dans votre navigateur.

C'est écrit en Rust, sans bibliothèque standard, avec de l'assembleur là où chaque cycle compte. Résultat : l'inventaire complet prend moins d'un dixième de seconde, et le programme entier tient dans moins de 1 Mo, environ 70 fois moins que UserDiag (57 Mo).

## Ce que Rustine analyse

| | |
| --- | --- |
| **Écrans bleus et plantages** | Lecture directe des vidages noyau : code d'arrêt, pilote mis en cause, erreurs matérielles WHEA. |
| **Santé des disques** | SMART et journal NVMe : usure, secteurs défectueux, température, données écrites. |
| **RAM et XMP/EXPO** | Barrettes, canaux, fréquence réelle, profil désactivé, kits mélangés. |
| **Où passe votre RAM** | Chaque page mémoire classée comme dans RAMMap, programmes et pilotes responsables, détection des vraies fuites. |
| **Latence des pilotes** | Les pilotes qui font craquer le son et saccader les jeux, comme LatencyMon. |
| **Températures** | Température et puissance du processeur, tenue sous charge. |
| **Vitesse** | Disques (séquentiel et 4K), carte graphique, transferts PCIe, débit Internet. |
| **Écrans et GPU** | Écran réglé sous sa fréquence max, carte graphique en x8, pilote planté. |
| **Réseau** | Lien Ethernet bloqué à 100 Mb/s, Wi-Fi faible, pertes de paquets. |
| **Santé de Windows** | Windows Update, sécurité, tâches et services qui tournent en douce, démarrage. |

## Quatre formules

| Formule | Durée | Contenu |
| --- | --- | --- |
| Sans test | ~2 s | Tout l'inventaire et les conseils, sans rien solliciter. |
| Rapide | ~10 s | En plus : fréquence réelle, calcul, caches et RAM, disque Windows, carte graphique. |
| Complet | ~1 min | En plus : tous les disques, débit Internet, 30 s de charge. |
| Long | ~5 min | Quatre minutes de charge avec courbe de température, tests disque plus longs. |

Le bouton **Analyser la mémoire** surveille la RAM pendant une minute pour repérer ce qui grossit, et compare avec l'analyse précédente pour confirmer une fuite.

## Vos données

Aucun numéro de série, nom de machine ni nom d'utilisateur n'est collecté, et les chemins de votre profil sont masqués.

Par défaut, le rapport est envoyé sur yatofix.com pour créer un lien public à partager, puis supprimé au bout de 180 jours. Votre rapport local contient un lien pour le supprimer vous-même. Pour rester hors ligne, décochez « Créer un lien public » ou lancez `Rustine.exe --hors-ligne`.

Rien ne reste installé sur votre PC. Seule exception, à votre demande : l'option « Températures » installe le pilote signé [PawnIO](https://pawnio.eu).

## Mises à jour

Rustine regarde ici, sur GitHub, si une version plus récente est sortie. Si oui, il vous la propose avec « Mettre à jour », « Plus tard » ou « Ne plus me rappeler », et garde un bouton **Mettre à jour** en haut de la fenêtre avec le nombre de commits de retard. La mise à jour télécharge le nouvel exécutable depuis la dernière [release](https://github.com/samirmedani/rustine/releases), vérifie son empreinte SHA-256, remplace l'ancien et relance Rustine. Rien n'est envoyé pour cela.

## Premier lancement : l'avertissement de Windows

Rustine n'est pas signé avec un certificat payant, donc Windows affichera probablement « Windows a protégé votre ordinateur ».

1. Dans le navigateur, choisissez **Conserver** si on vous le demande.
2. Sur l'écran SmartScreen, cliquez sur **Informations complémentaires**, puis **Exécuter quand même**.

Chaque version est analysée par Microsoft Defender avant sa mise en ligne. Vous pouvez vérifier votre fichier avec son empreinte SHA-256, publiée dans chaque [release](https://github.com/samirmedani/rustine/releases) :

```powershell
Get-FileHash .\Rustine.exe -Algorithm SHA256
```

## Configuration

Windows 11, 64 bits. Windows 10 peut fonctionner, sans garantie. Les droits administrateur sont demandés au lancement pour lire la santé des disques et les écrans bleus ; vous pouvez refuser, l'analyse continue en mode limité.

## Ligne de commande

| Option | Effet |
| --- | --- |
| `--sans-test` · `--rapide` · `--complet` · `--long` | Choisit la formule. |
| `--memoire` | Analyse de la mémoire (60 s de surveillance). |
| `--hors-ligne` | Aucun envoi, aucun accès Internet. |
| `--no-open` | N'ouvre pas le rapport dans le navigateur. |
| `--sans-admin` | Pas de demande de droits administrateur. |
| `--console` | Sortie texte dans le terminal. |
| `--mettre-a-jour` | Installe la dernière version publiée ici, puis quitte. |

## Bugs et idées

Ouvrez une [issue](https://github.com/samirmedani/rustine/issues) avec votre version de Windows et, si possible, le lien de votre rapport.

---

Rustine est gratuit et développé sur mon temps libre, édité par [Yatofix](https://yatofix.com). Le code source n'est pas publié ; le logiciel est distribué gratuitement, tous droits réservés.
