# Syslog

__System Logging protocol__ (SysLog), désigne un protocole standard qui sert à envoyer des fichiers du journal système ou des messages ayant trait à des événements à un serveur dédié appelé serveur syslog.

On l’utilise avant toute chose pour collecter différents journaux d’événements auprès de plusieurs machines et pour les transférer vers un emplacement central depuis lequel on pourra les consulter et les examiner.

## Les composants de syslog

Sur tous les types de périphériques, différents événements sont générés par le système à la suite de changements de situation. Ces événements sont en général enregistrés localement à un emplacement où l’administrateur pourra les consulter et les analyser. Cependant, examiner une importante quantité de journaux d’événements sur un nombre tout aussi élevé de routeurs, de switches et de systèmes prendrait un temps fou et s’avèrerait peu commode. Syslog remédie à ce problème en transférant ces événements vers un serveur centralisé.

## Comment ça marche ?

### Un message syslog se compose de 3 parties : 

#### 1) le **PRI** : **__(le niveau de priorité calculé)__** Les données PRI envoyées via le protocole syslog sont le fruit de deux valeurs numérales qui permettent de classifier le message.

- **0 -- (kern)** : Messages du noyau
- **1 -- (user)** : Messages de l’espace utilisateur
- **2 -- (mail)** : Messages du système de messagerie
- **3 -- (deamon)** : Messages des processus d’arrière-plan
- **4 -- (auth)** : Messages d’authentification
- **5 -- (syslog)** : Messages générés par syslogd lui-même
- **6 -- (lpr)** : Messages d’impressions
- **7 -- (nncp)** : Messages d’actualités
- **8 -- (uucp)** : Messages UUCP
- **9 -- (cron)** : Taches planifiées (at/cron)
- **10 -- (security)** : Sécurité / élévation de privilèges
- **11 -- (ftp)** : Logiciel FTP
- **12 -- (ntp)** : Synchronisation du temps NTP
- **13 -- ()** : Log audit
- **14 -- ()** : Log alert
- **15 -- (solaris cron)** : Taches planifiées pour solaris (at/cron)
- **16 - 23  -- (local0 ... local7)** : Utilisation locale 0 - 7

#### 2) le **HEADER** : **__(en-tête comportant les informations d’identification)__** La seconde partie d'un message syslog catégorise l'importance ou la gravité du message par un chiffre allant de 0 à 7
- **0 --	(Emergency)**	Système inutilisable.
- **1 --	(Alert)**	Une intervention immédiate est nécessaire.
- **2 --	(Critical)**	Erreur critique pour le système.
- **3 --	(Error)**	Erreur de fonctionnement.
- **4 --	(Warning)**	Avertissement (une erreur peut intervenir si aucune action n’est prise).
- **5 --	(Notice)**	Événement normal méritant d’être signalé.
- **6 --	(Informational)**	Pour information.
- **7 --	(Debug)**	Message de mise au point.

Les deux valeurs sont agrégées pour produire un indice de Priorité qui est envoyé conjointement au message. Cet indice se calcule en multipliant la catégorie par 8 et en y ajoutant le niveau de gravité. Plus le PRI est bas, plus la priorité est élevée.

<code>Priorité = (catégorie x 8) + gravité</code>



#### 3) le **MSG** : (le message lui-même)