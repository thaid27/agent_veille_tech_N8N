# Agent pour l'automatisation du processus de veille technologique 

Cet agent effectue une recherche hebdomadaire à propos des nouvelles sorties d'outils et de modèles d'IA générative. Pour cela, il se base sur une sélection de sources choisis dont il extrait les informations voulues et les rassemble afin de définir une description pour chaque outil présenté dans les sources. Chacune de ces descriptions est alors confronté à une base de données contenant les information des semaines passées afin de mettre à jour ces descriptions et d'éviter les redites avant d'y être stockées. Enfin, l'agent génère une newletter avec ces informations et l'envoie à une liste d'emails.   

## Fonctionnement détaillé de l'agent 

Gestion des sources : 
Les informations proviennent 


## Schéma de l'agent 

image

## Exemple de newletters 



## Plus value apporté 





---

# Reproduction

Le workflow n8n utilisé est disponible ici mais il est nécessaire d'ajouter les clés et endpoints de l'utilisateur pour les serives API utilisés (RapidAPI, YoutubeDataAPI, OpenAI, Gmail, . Pour la personalisation de l'agent, il est aussi possible de changer les sources récherchées afin de changer de sujet pour la newletters et les prompts afin de changer les informations à extraire. Enfin, le changement du format de mail en html est possible pour obtenir le visuel voulu pour la newsletters.   
