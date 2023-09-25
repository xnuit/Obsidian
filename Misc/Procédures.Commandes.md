## ***Déconnexion Outlook***
HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\Identity
DisableADALatopWAMOverride Value=1  
DisableAADWAM Value=1  
EnableADAL  Value=1  

Reset de la clé Office dans la BDR + déconnexion du/des compte(s) si présent dans les paramètres (cf screen 1) + check dans le mag et suppression des identifications Office comme le second screen + reboot.
Après le reboot, remettre les clés avec le script BDR_modifs_globalesetc….bat + reparamétrer le ou les comptes

## ***Install Win 11 sans Internet***
`Maj f10 OOBE \BYPASS NRO`

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