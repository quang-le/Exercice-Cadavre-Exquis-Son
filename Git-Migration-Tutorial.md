# Déplacer des dossiers d'un repo à un autre sans perdre l'historique

0. **En deux mots, il va falloir:**
- Cloner le repo d'origine dans un dossier local temporaire
- Isoler les fichiers à garder
- Copier les fichiers dans le repo de destination
- Faire un `git pull`

Il y a aussi  quelques précautions à prendre pour éviter que des erreurs de manipulation ne mettent le chaos dans le repo d'origine.

La méthode décrite ci-dessous est un résumé/traduction/compte-rendu d'expérience de la méthode décrite par *mcarans* sur [StackOverflow](https://stackoverflow.com/questions/1365541/how-to-move-files-from-one-git-repo-to-another-not-a-clone-preserving-history).

1. **Préparer les fichiers**
Soit A: le repo à déplacer
Et B, le repo de destination

- Clonez le repo en local et allez dedans:

`git clone <lien vers le repo A>`
`cd <dossier du repo A>`

Si vous avez déjà une copie du repo en local, je conseille de créer un dossier temporaire et d'y cloner A.

- Pour éviter les dégâts liés aux fausses manoeuvres, coupez le lien avec origin:

`git remote rm origin`

Maintenant, si ça foire, vous êtes *safe*.

- Si vous ne voulez déplacer qu'un dossier en particulier, la commande suivante permet de ne garder que le dossier voulu et son historique:

`git filter-branch --subdirectory-filter <~/dossier à garder> -- --all`

Note: Dans mon cas, cette commande livre un message d'erreur:

`fatal: <~/dossier à partager> est hors du dépôt`
`Could not get the commits`

Je n'ai pas trouvé ce qui causait cette erreur, mais ça n'a pas empĉhé la suite du processus de se dérouler correctement.

- L'étape précedente met tous les fichiers de votre dossier tels quels dans le dossier principal de votre repo. Vous pouvez les réorganiser avant la migration:

`mkdir <nouveau dossier>`
`mv * <nouveau dossier>`
`git add .`
`git commit -m "<description du commit>`

Pas besoin du `push` vu qu'on a plus de lien avec origin.

2. **La migration**

- Si vous ne l'avez pas en local, clonez le repo B:
`git clone <lien vers le repo B>`
`cd <dossier du repo B>`

- Créez une connection *remote* de B vers A (où A sera une branche de B):

`git remote add branche-A <chemin/local/vers/repoA>`

L'expression *branche-A* peut être ce que vous voulez, c'est une désignation arbitraire que vous choisissez. Faites court, ça vous fera gagner du temsp quand vous devrez le retaper.

La solution sur StackOverflow disait de mentionner le chemin vers le sous-dossier à transférer. Lors de ma tentative, cela donnait un message d'erreur. Si vous mentionnez le dossier du repo (le dossier principal qui est créer quand vous clonez), ça marche tout aussi bien.

- Faites un bon vieux pull:

`git pull branche-A master --allow-unrelated-histories`

IMPORTANT: il se peut que vous deviez mettre git à jour pour qu'il reconnaisse `--allow-unrelated-histories`. Sur Ubuntu, cela nécessite d'ajouter un repo:

`sudo add-apt-repository ppa:git-core/ppa`
`sudo apt-get update`
`sudo apt-get install git -y`

- Un peu de cleanup, et on push:

`git remote rm <branche-A>`
`git push`

Normalement, les fichiers sont sur votre repo B avec leur historique de commit. Si jamais ça a foiré, votre copie locale et votre repo sur GitHub sont *safe*.

Bon rangement!

*quang-le, 26/07/2018*
*Crédits: [http://gbayer.com/development/moving-files-from-one-git-repository-to-another-preserving-history/](http://gbayer.com/development/moving-files-from-one-git-repository-to-another-preserving-history/), [https://stackoverflow.com/questions/1365541/how-to-move-files-from-one-git-repo-to-another-not-a-clone-preserving-history](https://stackoverflow.com/questions/1365541/how-to-move-files-from-one-git-repo-to-another-not-a-clone-preserving-history).*


