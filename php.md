# Guide d'Intégration

Ce guide est fait à l'attention de votre technicien.

## Demander un paiement - Méthode 1

Pour initier une transaction, faites un simple appel HTTP de type Post vers le service web de PayGateGlobal et passer les paramètres requis.

### Services:

FLOOZ, TMONEY

### URL:

`https://paygateglobal.com/api/v1/pay`

### Methode:

HTTP Post

### Format d'échange de données:

JSON

### Paramètres:

| Nom          | Description                                                                              | Requis |
| ------------ | ---------------------------------------------------------------------------------------- | ------ |
| auth_token   | Jeton d’authentification de l’e-commerce (Clé API)                                       | OUI    |
| phone_number | Numéro de téléphone mobile du Client                                                     | OUI    |
| amount       | Montant de la transaction sans la devise (Devise par défaut: FCFA)                       | OUI    |
| description  | Détails de la transaction                                                                | NON    |
| identifier   | Identifiant interne de la transaction de l’e-commerce. Cet identifiant doit etre unique. | OUI    |
| network      | valeurs possibles: FLOOZ, TMONEY                                                         | OUI    |

### Réponse:

| Nom          | Description                                                                                                                                                                                                                                                         |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| tx_reference | Identifiant Unique générée par PayGateGlobal pour la transaction                                                                                                                                                                                                    |
| status       | Code d’état de la transaction. Les valeurs possible de la transaction sont: 0 : Transaction enregistrée avec succès, 2 : Jeton d’authentification invalide, 4 : Paramètres Invalides, 6 : Doublons détectées. Une transaction avec le même identifiant existe déja. |

## Demander un paiement - Méthode 2

Cette deuxième méthode permet de rediriger le client vers une page de paiement mise à votre disposition. Cette page est accessible via le lien ci dessous.

### Services:

FLOOZ, TMONEY

### URL:

`https://paygateglobal.com/v1/page`

### Methode:

HTTP Get

### Format d'échange de données:

QUERY STRING

### Paramètres:

| Nom         | Description                                                                                                                           | Requis |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| token       | Jeton d’authentification de l’e-commerce (Clé API)                                                                                    | OUI    |
| amount      | Montant de la transaction sans la devise (Devise par défaut: FCFA)                                                                    | OUI    |
| description | Détails de la transaction                                                                                                             | NON    |
| identifier  | Identifiant interne de la transaction de l’e-commerce. ex: Numero de commande. Cet identifiant doit etre unique.                      | OUI    |
| url         | Lien de la page vers laquelle le client sera redirigé après le paiement                                                               | NON    |
| phone       | Numéro de téléphone du client                                                                                                         | NON    |
| network     | Réseau du numéro de téléphone (ex: MOOV, TOGOCEL). Si ce parametre n'est pas fourni, le client devra manuellement choisir son réseau. | NON    |

### Redirection:

Le client sera redirigé vers une page de paygate global. exemple: `https://paygateglobal.com/v1/page?token=1234&amount=300&description=test&identifier=10`

## Recevoir une confirmation de paiement

Une fois le paiement effectué par le client, PayGateGlobal enverra un message de confirmation à l’URL de retour de l’e-commerce (Si précédemment fourni).

### Services:

FLOOZ, T-Money

### Methode:

HTTP Post

###
