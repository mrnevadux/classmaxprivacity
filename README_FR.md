# POLARIS Android — projet natif

Cette version Android est conçue comme un assistant vocal polyvalent utilisable immédiatement après configuration.
Elle comprend :
- Conversation française avec Gemini (API REST).
- Reconnaissance vocale Android à la demande et synthèse vocale française.
- Commandes locales sans Gemini : heure/date, ouvrir des sites, recherche web, musique YouTube/Spotify.
- Recherche d'informations via navigateur (résultats web, horaires, météo, etc.).
- Ouverture d'applications installées par leur nom (lancement via lanceur Android).
- Préparation de messages via le partage Android : l'utilisateur choisit l'application et valide l'envoi.
- Création de notes TXT/MD dans Documents/Polaris sans écrasement.
- Rappels locaux simples via AlarmManager/notifications (autorisation notifications requise).
- Historique local, thème sombre, réglages de clé Gemini, bouton micro stop.
- Actions annoncées seulement après lancement réussi ; Gemini ne peut pas lancer des actions arbitraires.

## Configuration et compilation
1. Ouvre le dossier `Polaris_Android` dans Android Studio (version récente).
2. Synchronise Gradle.
3. Lance sur un téléphone Android 8+ (Android 13+ recommandé).
4. Dans Réglages de l'app, colle ta clé Gemini AI Studio.
5. Autorise micro et notifications quand Android le demande.

Pour générer un APK : Android Studio > Build > Build APK(s).
Pour générer un AAB : Build > Generate Signed Bundle/APK > Android App Bundle.
Le workflow GitHub Actions compile un APK debug et un AAB release non signé pour distribution de test.

## Important : ce qui est réellement possible
- « Hey Polaris » permanent en arrière-plan n'est PAS activé dans cette version. Android restreint fortement le micro en arrière-plan. La version fournie utilise le bouton micro, qui est fiable et visible. Un vrai mot de réveil local Vosk nécessite ensuite un service au premier plan avec notification persistante, modèle français embarqué/téléchargé, et tests selon les fabricants/batterie.
- Le contrôle tactile de toutes les autres applications (lire l'écran, cliquer, saisir partout) nécessite un AccessibilityService activé volontairement par l'utilisateur. Il n'est pas inclus comme faux contrôle dans cette version.
- Les messages sont préparés dans l'application de partage ; tu choisis le destinataire et confirmes l'envoi.
- Les achats, paiements, création de compte et formulaires sensibles restent manuels et soumis à confirmation.
- La clé Gemini est conservée dans les préférences privées de l'application, mais une application cliente ne peut pas rendre une clé API totalement secrète. Pour une diffusion publique, utiliser un backend personnel avec authentification et quotas.
- La clé n'est jamais envoyée dans le dépôt GitHub par ce projet.
- Aucun accès root, aucune modification système, aucun démarrage automatique, aucune suppression de fichiers.

## Exemples de commandes
« Quelle heure est-il ? »
« Ouvre YouTube »
« Recherche les horaires du cinéma de Thonon »
« Mets Michael Jackson sur Spotify »
« Cherche les horaires du prochain train pour Genève »
« Prépare un message pour dire que j'arrive dans dix minutes »
« Crée une note appelée idées avec mes idées pour Polaris »
« Rappelle-moi d'appeler Paul à 18 heures »
Pour toute demande générale, Polaris utilise Gemini. Les recherches/actions web passent par le navigateur Android ; le contenu des pages est traité comme donnée, pas comme instruction.
