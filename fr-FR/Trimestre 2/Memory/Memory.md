---
title: Memory
level: Scratch 2
language: fr-FR
stylesheet: scratch
embeds: "*.png"
materials: ["Club Leader Resources/*"]
...
stylesheet: scratch
embeds: ".png"
materials: ["Club Leader Resources/.*"]
base: https://github.com/CodeClub/scratch-curriculum/blob/master/en-GB/Term%202/Memory/Memory.md

translators: Hibouu,
reviewer: Céline
status: free ...

## Community Contributed Project { .challenge .pdf-hidden }
Ce projet a été créé par Erik et sa fille Ruth. Si vous souhaitez apporter votre propre contribution, alors [Contactez nous sur Github](https://github.com/CodeClub).

# Introduction { .intro }

Dans ce projet, tu vas créer un jeu de mémoire dans lequel il faut mémoriser et répéter une séquence de couleurs produite au hasard !

<div class="scratch-preview">
  <iframe allowtransparency="true" width="485" height="402" src="http://scratch.mit.edu/projects/embed/34874510/?autostart=false" frameborder="0"></iframe>
  <img src="colour-final.png">
</div>

# Étape 1 : Des couleurs au hasard { .activity }

D'abord, il faut créer un lutin qui peut changer de couleur au hasard, pour que le joueur puisse le mémoriser.

## Liste d'activités { .check }

+ Démarre un nouveau projet Scratch et supprime le lutin chat pour que ton projet soit vide. Tu peux trouver l'éditeur Scratch à l'adresse <a href="http://jumpto.cc/scratch-new">jumpto.cc/scratch-new</a>.

+ Choisi un lutin et un arrière-plan. Ce lutin n'est pas forcément une personne, mais il doit pouvoir afficher différentes couleurs.

	![screenshot](colour-sprite.png)

+ Dans ton jeu, pour chaque couleur, tu vas utiliser un chiffre différent :

	+ 1 = rouge ;
	+ 2 = bleu ;
	+ 3 = vert ;
	+ 4 = jaune.

	Donne à ton lutin 4 costumes de couleur différente, un pour chaque couleur ci-dessus. Vérifie que tes costumes colorés soient dans le même ordre que les couleurs de la liste ci-dessus.

	![screenshot](colour-costume.png)

+ Pour créer un changement au hasard, tu as besoin de créer une __liste__. Une liste est une variable qui enregistre beaucoup de données __dans l'ordre__. Crée une nouvelle liste appelée `séquence` {.blockdata}. Comme seul ton lutin a besoin de voir la liste, tu peux cliquer sur  'Pour ce lutin uniquement'.

	![screenshot](colour-list.png)

	Tu dois maintenant voir ta liste vide en haut à gauche de la scène, ainsi que beaucoup de nouveaux blocs à utiliser avec la liste.

	![screenshot](colour-list-blocks.png)

+ Ajoute ce code à ton lutin, pour ajouter un chiffre au hasard à ta liste (et affiche le bon costume) 5 fois :

	```blocks
		quand le drapeau vert pressé
		supprimer l'élément (tout v) de la liste [séquence v]
		répéter (5) fois
			ajouter (nombre aléatoire entre (1) et (4)) à [séquence v]
			basculer sur costume (élément (dernier v) of [séquence v]
			attendre (1) secondes
		fin
	```

	Note que tu as également vidé la liste au début.

## Défi : ajouter du son {.challenge}
Testes ton projet plusieurs fois. Tu remarques que parfois le même numéro est choisi deux (ou plusieurs) fois dans la même séquence, ce qui la rend plus difficile à mémoriser. Peux-tu ajouter un bruit de tambour chaque fois que le lutin change de costume ?

Peux-tu ajouter un autre son de tambour en fonction du numéro choisi au hasard ? Ce code devrait être _très_ proche de celui utilisé pour changer de couleur.

## Enregistre ton projet { .save }

# Étape 2 : Répéter la séquence { .activity }

Ajoute 4 boutons pour que le joueur indique la séquence dont il se souvient.

## Liste d'activités { .check }

+ Ajoute 4 lutins à ton projet, qui deviendront des boutons. Modifie tes 4 lutins de façon à ce qu'il y en ait un pour chacune des couleurs.

	![screenshot](colour-drums.png)

+ Quand le tambour rouge est cliqué, tu dois envoyer un message à ton lutin, pour lui faire savoir que le bouton rouge a été cliqué. Ajoute ce code à ton tambour rouge:

	```blocks
		quand ce lutin est cliqué
		envoyer à tous [rouge v]
	```

+ Quand ton lutin reçoit ce message, il doit vérifier si le numéro 1 est au début de la liste (ce qui signifie que le rouge est la couleur suivante dans la séquence). Si oui, tu peux supprimer le numéro de la liste car il a été deviné correctement. Sinon, c'est la fin du jeu.

	```blocks
		quand je reçois [rouge v]
		si <(élément (1 v) de [séquence v])=[1]> alors
			supprimer l'élément (1 v) de la liste [séquence v]
		sinon
			dire [Fin du jeu !] pendant (1) secondes
			stop [tout v]
		fin
	```

+ Tu peux également afficher des lumières étincelantes quand la liste est vide, pour montrer que toute la séquence a été correctement mémorisée. Ajoute ce code à la fin du script du lutin `quand le drapeau vert pressé` {.blockevents} :

	```blocks
		attendre jusqu'à < (longueur de [séquence v]) = [0]>
		envoyer à tous [gagné v] et attendre
	```

+ Clique sur la scène, et ajoute ce code pour que la couleur de l'arrière-plan change une fois que le joueur a gagné.

	```blocks
		quand je reçois [gagné v]
		jouer le son [drum machine v]
		répéter (50) fois
			ajouter à l'effet [couleur v] (25)
			attendre (0.1) secondess
		fin
		annuler les effets graphiques
	```

## Défi : Créer 4 boutons {.challenge}
Répétez les étapes ci-dessus pour vos boutons bleus, verts et jaunes . Quel code reste le même, et quel code va changer pour chaque bouton ?

Tu peux aussi ajouter des sons quand le bouton est pressé.

N'oublie pas de tester le code que tu as ajouté ! Peux-tu mémoriser une séquence de 5 couleurs ? La séquence est-elle différente à chaque fois ?

## Enregistre ton projet { .save }

# Étape 3 : Créer plusieurs niveaux { .activity .new-page }

Jusqu'à présent, le joueur ne devait se souvenir que de 5 couleurs . Améliorons le jeu, de façon à ce que la longueur de la séquence augmente à chaque fois.

## Liste d'activités { .check }

+ Crée une nouvelle variable appelé `score` {.blockdata}.

	![screenshot](colour-score.png)

+ Ce `score` {.blockdata} sera utilisé pour déterminer la longueur de la séquence que le joueur devra mémoriser. Donc, pour commencer, le score (et la longueur de la séquence) est 3. Ajoute ce bloc de code sur le lutin au début de `quand le drapeau vert pressé` {.blockevents} :

	```blocks
		mettre [score v] à [3]
	```

+ Au lieu de créer toujours une séquence de 5 couleurs, tu veux maintenant utiliser le  ` score` {.blockdata}  pour déterminer la longueur de la séquence. Change la boucle `répéter` {.blockcontrol} de ton lutin (pour la création de la séquence) en:

	```blocks
		répéter (score) fois
		fin
	```

+ Si la séquence est correctement mémorisée, il faut ajouter 1 au score, pour augmenter la longueur de la séquence.

	```blocks
		ajouter à [score v] (1)
	```

+ Pour finir, tu dois ajouter la boucle `répéter indéfiniment` {.blockcontrol} autour du bloc de code pour générer la séquence, de sorte qu'une nouvelle séquence est créée pour chaque niveau. Voici à quoi le code de ton objet devrait ressembler:

	```blocks
		quand le drapeau vert pressé
		mettre [score v] à [3]
		répéter indéfiniment
			supprimer l'élément (tout v) de la liste [séquence v]
			répéter (score) fois
				ajouter (nombre aléatoire entre (1) et (4)) à [séquence v]
				basculer sur costume (élément (dernier v) de [séquence v]
				attendre (1) secondes
			fin
			attendre jusqu'à < (longueur de [séquence v]) = [0]>
			envoyer à tous [gagné v] et attendre
			ajouter à [score v] (1)
		fin
	```

+ Demande à tes amis de tester ton jeu. N'oublie pas de cacher la liste `séquence` {.blockdata}   avant qu'ils jouent !

## Enregistre ton projet { .save }

# Étape 4 : Meilleur score { .activity }

Maintenant enregistre le meilleur score pour pouvoir jouer contre tes amis.

## Liste d'activités { .check }

+ Ajoute 2 nouvelles variables à ton projet, que tu vas appeler `meilleur score` {.blockdata} et `nom` {.blockdata}.

+ Si jamais le jeu se finit (en appuyant sur le mauvais bouton), tu dois vérifier si le score du joueur est meilleur que le meilleur score actuel. Si c'est le cas, tu dois enregistrer le score du joueur en tant que le meilleur score, et enregistrer le nom du joueur. Voici à quoi ton bouton rouge devrait ressembler:

	```blocks
		quand je reçois [rouge v]
		si <(élément (1 v) de [séquence v])=[1]> alors
			supprimer l'élément (1 v) de la liste [séquence v]
		sinon
			dire [Fin du jeu !] pendant (1) secondes
			si < (score) > (meilleur score) > alors
				mettre [meilleur score v] à (score)
				demander [Meilleur score ! Quel est ton nom ?] et attendre
				mettre [nom v] à (réponse)
			sinon
			stop [tout v]
		fin
	```

+ Tu as besoin d'ajouter ce nouveau code au 3 autres boutons ! As-tu remarqué que le code ' Fin du jeu !' de chacun des 4 boutons est exactement le même?

	![screenshot](colour-same.png)

+ Si jamais tu as besoin de changer quelque chose dans ce code, comme l'ajout d'un son ou changer le message 'Fin du jeu !', tu dois le changer 4 fois ! Cela peut parfois être ennuyeux, et te faire perdre beaucoup de temps.

A la place, tu peux définir tes propres blocs, et les réutiliser dans ton projet ! Pour ce faire, clique sur `Ajouter blocs` {.blockmoreblocks}, puis ' Créer un bloc '. Appelle ce nouveau bloc 'Fin du jeu'.

	![screenshot](colour-more.png)

+ Ajoute le code du block `sinon` {.blockcontrol} du bouton rouge dans le nouveau bloc qui vient d'apparaître :

	![screenshot](colour-make-block.png)

+ Tu as créé une _nouvelle_fonction appelée `Fin du jeu` {.blockmoreblocks}, que tu peux utiliser partout où tu veux. Ajoute ton nouveau bloc  `Fin du jeu` {.blockmoreblocks} aux 4 scripts des boutons.

	![screenshot](colour-use-block.png)

+ Maintenant ajoute un son pour quand le mauvais bouton est pressé. Tu as seulement besoin d'ajouter ce bloc de code _une fois_ dans le bloc `Fin du jeu` {.blockmoreblocks} que tu as fait, et pas 4 fois !

	![screenshot](colour-cough.png)

## Défi : Fais plus de blocs {.challenge}
As-tu remarqué d'autres blocs de code qui seraient les mêmes pour les 4 boutons ?

![screenshot](colour-more-blocks.png)

Peux-tu créer un autre bloc personnalisé, qui serait utilisé par chaque bouton ?

## Enregistre ton projet { .save }

## Défi : Autre costume {.challenge}
As tu remarqué que le jeu commence avec ton lutin montrant une des 4 couleurs, et que c'est toujours la dernière couleur de la séquence qui est affiché quand le joueur répète la séquence ?

Peux-tu ajouter un autre costume blanc à ton lutin, qui sera affiché au début de ton jeu, et quand le joueur essaye de copier la séquence ?

![screenshot](colour-white.png)

## Enregistre ton projet { .save }

## Défi : Niveau de difficulté {.challenge}
Peux-tu permettre au joueur de choisir entre un 'mode facile' (utilise seulement les tambours rouge et bleu) et le mode 'mode normal' (qui utilises les 4 tambours)?

Tu peux même ajouter un mode 'difficile', qui aura un 5e tambour!

## Enregistre ton projet { .save }
