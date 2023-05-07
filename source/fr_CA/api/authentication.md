---
extends: _layouts.developer_resources
section: content
locale: fr_CA
---

# Authentification

## Essentiels pour la connexion

Le minimum requis pour l'authentification à l'API sont les champs courriel et mot de passe

```
curl -X POST 'http://ninja.test/api/v1/login' \
-H "Content-Type:application/json" \
-d '{"email":"demo@invoiceninja.com","password":"Password0"}' \
-H "X-Requested-With: XMLHttpRequest";
```
La réponse de retour est un objet CompanyUser qui contient des relations enfant de ,utilisateur / entreprise et ses entités associées

[truncated response]

```
 	{
        "permissions": "",
        "notifications": {
            "email": []
        },
        "settings": {},
        "is_owner": true,
        "is_admin": true,
        "is_locked": false,
        "updated_at": 1631673918,
        "archived_at": 0,
        "created_at": 1631673918,
        "permissions_updated_at": 1631709918,
        "ninja_portal_url": "",
        "user": {
            "id": "q9wdL84djP",
            "first_name": "Price Strosin",
            "last_name": "Dr. Estrella Ortiz",
            "email": "small@example.com",
            "last_login": 1631674051,
            "oauth_user_token": "",
            "company_user": {
                "permissions": "",
                "notifications": {
                    "email": []
                },
                "settings": {},
                "is_owner": true,
                "is_admin": true,
                "is_locked": false,
                "updated_at": 1631673918,
                "archived_at": 0,
                "created_at": 1631673918,
                "permissions_updated_at": 1631709918,
                "ninja_portal_url": ""
            }
        },
        "company": {
            "id": "kQBeX78dyK",
            "company_key": "vlyh36bobfixnoyxdd6jkahdfwdse77glu5pgbjwqlurraqpphx3zdoce5batvx2",
            "update_products": true,
            "subdomain": "",
            "portal_mode": "domain",
            "portal_domain": "http:\/\/ninja.test:8000",
            "settings": {
                "auto_archive_invoice": false,
                "lock_invoices": "off",
            }
            "documents": [],
            "users": [
                {
                    "id": "q9wdL84djP",
                    "first_name": "Price Strosin",
                    "last_name": "Dr. Estrella Ortiz",
                    "email": "small@example.com",
                    "has_password": false,
                    "oauth_user_token": "",
                    "company_user": {
                        "permissions": "",
                        "notifications": {
                            "email": []
                        },
                        "settings": {},
                        "is_owner": true,
                }
            ],
            "designs": [],
            "clients": [],
            "invoices": [],

```

Vous pouvez ajouter des paramètres de requêtes qui peuvent inclure des informations additionnelles dans la réponse.

```
http://ninja.test/api/login?include_static=true
```

Ceci permettra d'inclure un étalage (array) de données (dateheure / conditions de paiement et autres données "statique" qui sont utilisées dans les sélecteurs du panneau d'administration) situé [ici](https://github.com/invoiceninja/invoiceninja/blob/v5-stable/app/Utils/Statics.php)

## X-API-SECRET header

Pour améliorer la résilience du routage de la connexion, vous pourriez aussi ajouter une en-tête additionnelle

```
X-API-SECRET
```

Cette valeur devrait correspondre à la variable dans .env

```
API_SECRET
```

Voici un exemple d'une connexion utilisant X-API-SECRET:


```
curl -X POST 'http://ninja.test/api/v1/login' \
-H "Content-Type:application/json" \
-d '{"email":"demo@invoiceninja.com","password":"Password0"}' \
-H "X-API-SECRET: SuperSecretSecret" \
-H "X-Requested-With: XMLHttpRequest";
```