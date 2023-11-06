## ***Déconnexion Outlook***

###### `HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\Identity `
DisableADALatopWAMOverride Value=1  
DisableAADWAM Value=1  
EnableADAL  Value=1  

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
 **HKLM\SOFTWARE\Policies\Microsoft\Windows\WorkplaceJoin, “BlockAADWorkplaceJoin”=dword:00000001**

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