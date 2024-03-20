# Symptômes :

Erreurs 1001 ou multiples demandes de mots de passe intempestifs avec l’agent Trend Micro installé et que vous avez exclu toutes les autres pistes (Ex : BDR de l’Office « ADAL, etc… »).
 
# Résolution :

Il faut se connecter sur la console Trend Micro puis aller éditer la ou les stratégies dont vous avez besoin. (Ex : Serveurs & PC)
Les modifications à apporter sont situés dans Antivirus/Anti-programme Espion, Surveillance des comportements, Programme sécurisé et URL approuvées/bloquées.
### •	Antivirus/Anti-programme Espion, Il faut exclure :
o	Deux répertoires :
```
-	C:\Users\*\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy*
```

```
C:\Windows\SystemApps\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy*
```
NB : Les étoiles sont gérées dans Trend Micro et signifie tout caractère.
o	Un fichier .exe : 
```
C:\Windows\SystemApps\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\Microsoft.AAD.BrokerPlugin.exe
```
 ![[Pasted image 20240320145317.png]]
Aller en bas de page pour enregistrer les modifications sinon elles ne seront pas prises en compte quand vous changer de menu.
 
 
### •	Surveillance des comportements, il faut approuver :
o	Un fichier .exe : 

```
C:\Windows\SystemApps\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\Microsoft.AAD.BrokerPlugin.exe
``` 

![[Pasted image 20240320145329.png]]
Aller en bas de page pour enregistrer les modifications sinon elles ne seront pas prises en compte quand vous changer de menu. 
### •	Programme sécurisé, il faut approuver :
Un fichier .exe 
```
C:\Windows\SystemApps\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\Microsoft.AAD.BrokerPlugin.exe
```
![[Pasted image 20240320145339.png]]
Aller en bas de page pour enregistrer les modifications sinon elles ne seront pas prises en compte quand vous changer de menu.
 
 
### •	URL approuvées/bloquées, il faut approuver :
o	Deux URL : http://autodiscover.nomdedomaine.com et https://autodiscover.nomdedomaine.com où nomdedomaine.com est le nom de domaine du client.
 ![[Pasted image 20240320145346.png]]
Aller en bas de page pour enregistrer les modifications sinon elles ne seront pas prises en compte quand vous changer de menu.
 
Sources : https://success.trendmicro.com/dcx/s/solution/000292628?language=en_US
