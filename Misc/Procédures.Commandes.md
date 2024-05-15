## ***Déconnexion Outlook***

###### `HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\Identity `
DisableADALatopWAMOverride Value=1  
DisableAADWAM Value=1  
EnableADAL  Value=1  

(Déconnecter tous les comptes dans compte et mails + credential manager
refaire un nouveau profil
re-paramétrer les boites mails et les fichiers de données.)
Reset de la clé Office dans la BDR + déconnexion du/des compte(s) si présent dans les paramètres (cf screen 1) + check dans le mag et suppression des identifications Office comme le second screen + reboot.
Après le reboot, remettre les clés avec le script BDR_modifs_globalesetc….bat + reparamétrer le ou les comptes

## ***Install Win 11 sans Internet***
`Maj f10 -> OOBE \BYPASS NRO`

## ***Lenteurs windows***
Si vous avez des bugs sur Windows, lenteurs ou plantages, vous pouvez passer ces petites cmd en admin évidemment 😊
`Dism /Online /Cleanup-Image /ScanHealth
`Dism /Online /Cleanup-Image /RestoreHealth
`sfc /scannow


## ***Outlook erreur 1001***
Supprimer tous les comptes dans windows professionnels,  scolaire et messagerie.
Supprimer dans SAM les logins
Redémarrer le poste

## Outlook crash réunion
Aller dans outlook fichier>options>compléments soit désactiver teams add-in
soit aller dans fichier>option>calendrier désactiver transformer en lien teams automatiquement.

## Ouvrir fichier partagés management
fsmgmt.msc


## Installation Imprimante Kyocera
``X:\5.Technique\IMPRESSION\Imprimantes & Copieurs\_Scripts_Installation_Kyocera
Copier le script dans le C:\abs client
cherche le _deploy-printer_ dans le sous dossier 64 bits
le lancer avec alt click en tant que ``.\adminabs
choisir le nom
trouver l'IP dans les propriétés de l'imprimante
mettre la file d'attente
rechercher le nom de l'impriuman,te dans le fiuchier texte qui apparait
installer et attente la fin
Attention au mode de selection dans le terminal
kini5892

## Désactiver la fenêtre "autoriser l'organisation à gérer les appareils ou se connecter à cette application uniquement."
 ```
 HKLM\SOFTWARE\Policies\Microsoft\Windows\WorkplaceJoin, “BlockAADWorkplaceJoin”=dword:00000001
```

```
REG ADD HKLM\SOFTWARE\Policies\Microsoft\Windows\WorkplaceJoin /v "BlockAADWorkplaceJoin" /t REG_DWORD /d "1" /f
```

## DISABLE UAC : 
```
REG ADD HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v "EnableLUA" /t REG_DWORD /d "0" /f
```

## Task kill
```
taskkill /im <process> /f
```

## Script regedit key Office 365
```
d:\datas\5.Technique\INFRASTRUCTURE ET RESEAU\Procédures\Office\Office 2016
```

## Mise à jour temps NTP pour Domain Controller
```netdom query fsmo ``` Trouver le domain controller
```net stop w32time ``` Stopper le service de temps
```w32tm /config /syncfromflags:manual /manualpeerlist:"0.ca.pool.ntp.org"``` config ntp
```w32tm /config /reliable:yes``` Ajouter en source de confiance
```net start w32time``` Relancer service temps
```w32tm /resync /force``` Synchro
```w32tm /query /status``` Voir le statut
```w32tm /resync /nowait``` synchro les pc

## Get domain name
```
wmic computersystem get domain
```

## Problème fichier excel ouvert par autre utilisateur
### 1
Démarrez l’explorateur Windows et naviguez dans le répertoire contenant votre fichier Excel impacté par le problème.
Dans la fenêtre de l’explorateur Windows, cliquez sur l’onglet « Affichage », puis cliquez sur « Options » :
Cliquez sur l’onglet « **Affichage**« , puis cochez la case « **Afficher les fichiers, dossiers et lecteurs cachés** » et décochez la case « **Masquer les fichiers protégés du système d’exploitation**« . Validez en cliquant sur « OK »
Si le fichier temporaire d’Excel est corrompu, il est possible qu’il soit toujours présent dans le répertoire alors que toutes les instances du fichier sont fermés. Vérifiez la date de dernière modification… Il est fort probable qu’elle ne date pas du jour :
Éditez le fichier temporaire nommé **~$[Nom-du-fichier]** avec un éditeur de texte (Notepad, Notepad++, ou autres). Vous y trouverez sans doute le nom du dernier utilisateur ayant verrouillé le fichier avant le crash. S’agit-il du nom constamment affiché en verrouillage lorsqu’un utilisateur modifie votre fichier Excel ? Probable… :
Fermez votre fichier Excel et supprimez tout simplement le fichier temporaire.
### 2
Gestion de l'ordinateur > dossiers partagés > fichiers ouverts > Trouver l'arborescence.

## Imprimante vider file d'impression spooler
Se connecter au serveur (rds) ou est installée l'imprimante
`net stop spooler & del c:\Windows\System32\spool\PRINTERS\*.* /F /Q & net start spooler`

## Outlook force mode offline ou online.
Chemin de la clé 
`“HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Outlook\Profiles\Outlook\0a0d020000000000c000000000000046”
`
Nom de la clé : 00030398 et la valeur est « 01 00 00 00 » pour travailler en offline.
Par défaut c’est « 02 00 00 00 » pour travailler online.
![[Pasted image 20231211084657.png]]

## Supprimer une imprimante en cmd powershell
### cmd
`wmic printer get name`
`printui.exe /dl /n "PRINTER"`

### PS1
`Get-Printer | Format-List Name`
`Remove-Printer -Name "PRINTER"`

## Word n'imprime plus les images
Word n'affiche plus les images que ce soit dans l'aperçu d'impression ou pour une conversion en pdf.
`Fichier > options > option avancées > Impression > Cocher imprimer les images`

## Rediriger tous les postes dans l'OU Ordinateurs
```

redircmp "OU=Ordinateurs,OU=Domaine Proaxion,DC=domaine,DC=local"
Dsa.msc > affichage > avancé > propriétés UO souhaitée > editeur d'attributs > distinguished name > afficher.
```
## Autoriser les chemins longs (longpaths)
### powersell (5.1 minimum)
```
Set-ItemProperty 'HKLM:\System\CurrentControlSet\Control\FileSystem' -Name 'LongPathsEnabled' -value 1
```
### cmd
```
REG ADD HKLM\System\CurrentControlSet\Control\FileSystem /v "LongPathsEnabled" /t REG_DWORD /d "1" /f
```

## Vider le dossier spooler
```
net stop spooler & del c:\Windows\System32\spool\PRINTERS\*.* /F /Q & net start spooler
```

## Get serial number numéro de série machine
```
wmic bios get serialnumber
```

## Bug ou lenteurs windows
Si vous avez des bugs sur Windows, lenteurs ou plantages, vous pouvez passer ces petites cmd en admin évidemment 😊
```
Dism /Online /Cleanup-Image /ScanHealth
Dism /Online /Cleanup-Image /RestoreHealth
sfc /scannow

```

## Installation mails mdaemon
compte de messagerie > configuration manuelle des serveurs > autre
Autres > désac maj auto
Gestion de la base de données >  décocher les trois case
serveur imap = smtp = vm mail

## Installation TrendMicro Server/Agent
\\srv-adds > ofscan>Download > AgentX64

## Outlook désactiver la recherche sur serveur
**DisableServerAssistedSearch**
Key: HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Outlook\Options\Search  
Value name: **DisableServerAssistedSearch**  
Value type: REG_DWORD  
Value: 1

(You may need to manually create the registry key it it doesn't exist.)

## Enlever une ancienne adresse principale outlook registre regedit
**Outlook 2016** – `HKEY_CURRENT_USER \ Software \ Microsoft \ Office \ 16.0 \ Outlook \ Profiles
press **Ctrl + F**
search for **001f6641**
clicker sur la  clef pour voir si l'adresse est bien celle qu'on veut retirer

## Restauration windows si chiffrement BitLocker
Si le disque est chiffré les points de restaurations ne seront pas accessibles.
Il ya deux types de chiffrement BitLocker : Avec une clef de récupération ou sans clef de récupération via la TPM. La TPM contient la clef de chiffrement si le disque est retiré de la carte mère ou celle-ci grille il sera impossible de déchiffrer le disque.
manage-bde

## Licences CAL pour RDS/TSE
Admin Panel Office365 > Admin center > Vos produits > Logiciel.> Afficher les clefs d'activation > copier la clef dans le presse papier
Aller sur le serveur RDS ouvrir outils d'administration > Outils > Remote Desktop > Services
Clic droit sur le serveur installer les licences puis suivre les étapes.

## Déconnecter ghost connection fichier partage

```
net use * /del
net use \\srv-mdt /user:testtest
net use * /del
```

## Changer la langue du système windows
### powershell
```
Get-WinSystemLocale
```
```
Set-WinSystemLocale fr-FR
```

## Réparer et vider le cache outlook mail mdaemon
```
Se rendre dans C:\Users\"nom_user"\Appdata\Roaming\Alt-N\Outlook Connector 2.0\Accounts\"nom_profil"\"adresse_mail"
```
Supprimer attachments et localeCache.db mais **garder config.xml**

## Freeze sur TSE RDS pour un seul utilisateur
passer le bureau a distance en TCP
```
reg add "HKLM\software\policies\microsoft\windows nt\Terminal Services\Client" /v fClientDisableUDP /d 1 /t REG_DWORD
```

## Forcer la fermeture du spooler pour vider la file d'attente d'impression
```
net stop spooler
WINDOWS\System32\spool\PRINTERS
supprimmer tous les SHD et SPL
net start spooler
```

## Remettre l'autocompletion outlook des adresses mails
```
Ouvrir %LOCALAPPDATA%\Microsoft\Outlook
dupliquer le dossier stream autocomplete actuel
Ouvrir outlook sur le nouveau profil
Laisser Outlook OUVERT
écrire un nouveau mail avec une adresse, cela génère un nouveau fichier autocomplete
Copier le nom du fichier autocomplete le plus récent et renommer en .old
Copier le nom du nouveau fichier sur le fichier original (le plus volumineux)
```

## Fermer un fichier dans dossier partage bloque par ghost user
```
Win + r
fsmgmt.msc
fichiers ouverts
rechercher l'arborescence et fermer le fichier concerné
```
 
Il faut créer/modifier cette clé en DWORD "EnablePerUserCatalog" avec la valeur "0" dans ```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Search```

Une fois cette clé créer/modifier, il faut juste reboot le service Windows Search + rebuild l’indexation et c'est good.
 
Cela permet d’activer les options de recherches Outlook (qui sont grisés dans le cas contraire) et de faire refonctionner l’indexation sur un serveur RDS. Cf ci-dessous.
 ![[Pasted image 20240408081524.png]]
 ![[Pasted image 20240408081531.png]]
 
Enfaite cette clé si elle n'existe pas ou si elle est à 1, elle active le service d'indexation par utilisateur et non serveur ce qui crée un petit fichier .edb sur chaque profil utilisateur et si j'ai bien compris ce fichier est reset à chaque fermeture de session ou peut se reset donc pas ouf et accessoirement en fermeture de session peut te bloquer avec un process Windows Search sans que tu puisses forcer la déconnexion (hors stop service). (lol)
Ce n'est pas un bug c'est juste Microsoft qui pensait avoir eu l'idée du siècle mais pas moyen de modifier cette option en interface graphique ou en cmd ou en gpo, il faut créer/modifier la clé de registre…
 
## Installation de Windows 11 Pro changement de licence

Si la clef d'activation ne fonctionne pas, mettre cette clef générique pour la mise à niveau puis activer la licence avec la bonne clef ensuite.

**Clé générique: DYNDG-6CVGG-3HB9V-6TC8C-3YH26**


