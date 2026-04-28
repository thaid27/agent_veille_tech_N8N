# Agent pour l'automatisation du processus de veille technologique 

Cet agent effectue une recherche hebdomadaire à propos des nouvelles sorties d'outils et de modèles d'IA générative. Pour cela, il se base sur une sélection de sources choisis dont il extrait les informations voulues et les rassemble afin de définir une description pour chaque outil présenté dans les sources. Chacune de ces descriptions est alors confronté à une base de données contenant les information des semaines passées afin de mettre à jour ces descriptions et d'éviter les redites avant d'y être stockées. Enfin, l'agent génère une newletter avec ces informations et l'envoie à une liste d'emails.   

## Fonctionnement détaillé de l'agent 

**Gestion des sources :**

Les informations proviennent de deux types de sources necessitant un traitement différent pour obtenir les éléments recherchés :
- site web et blogs : traitement du flux rss pour récupérer le champ contenant le texte de la page
- chaines youtube orienté technologies IA :
    - utilisation de YoutubeDataAPI (API officiel de youtube) pour récupérer les identifiants des vidéos de la chaines sortie cette semaine ainsi que la description des vidéos contenant les liens des outils présentés 
    - les transcriptions issues de la génération automatique de youtube sont alors récupérées via une API externe hébergée sur RapidAPI (non récupérable via YoutubeDataAPI)

**Traitement des données bruts :**

À l'issue de la première étape, on obtient des données textes sous forme de transcriptions et d'articles. Un premier LLM extrait l'information concernant chaque outils cités dans ces sources et la formatte pour obtenir les éléments attendues pour chacun (nom, description, charactéristiques principales, éléments différenciants, comparaison avec d'autres outils du même type, lien). Ici et par la suite, le LLM utilisé est GPT-5-mini hebergé sur Azure. 

Une deuxième passe dans le LLM est effectué fournissant l'ensemble des descriptions d'outils afin de rassembler celles concernant les mêmes. Cette étape est effectué en deux temps par soucis de limite de tokens d'entrée pour le LLM et de perte d'informations liées à un trop gros nombre de tokens d'entrée. 

**Comparaison avec la base de données et mise à jour des descriptions**

Chaque description obtenue est confrontée à une base de données Azure Search contenant les descriptions des semaines précédentes pour éviter les redites par rapport aux précédentes newsletters, tout en permettant de mettre à jour les informations concernant ces outils avec d'éventuels nouveaux éléments évoquées cette semaine à leur sujet. Les nouveaux outils et mises à jour sont envoyés à la base de données. 

**Génération de la newsletter**

Enfin les descriptions d'outils sont rassemblés afin de générer une newsletter 


## Schéma de l'agent 

image

## Exemple de newletters 

image

## Plus value apporté 

Une recherche précise et détaillé par le choix des sources d'informations de confiance et des éléments d'importance
Vérification avec la base de données pour avoir des informations à jour concernant les technologies recherchées ainsi 



---

# Reproduction

Le workflow n8n utilisé est disponible ici mais il est nécessaire d'ajouter les clés et endpoints de l'utilisateur pour les serives API utilisés (RapidAPI, YoutubeDataAPI, OpenAI, Gmail, . Pour la personalisation de l'agent, il est aussi possible de changer les sources récherchées afin de changer de sujet pour la newletters et les prompts afin de changer les informations à extraire. Enfin, le changement du format de mail en html est possible pour obtenir le visuel voulu pour la newsletters.   
