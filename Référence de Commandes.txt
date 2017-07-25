Référence de Commandes
======================

Lancer le serveur Rails :

	rails server  # (`rails s`)

Ouvrir un REPL :

	rails console  # (`rails c`)

Voir les routes :

	rails routes


## Générateurs

`rails g model NOM_DU_MODELE [ARGUMENTS]`  
`rails g controller NOM_DU_CONTROLLEUR [ARGUMENTS]`  
`rails g migration NOM_DE_LA_MIGRATION [ARGUMENTS]`


## Migrations

Migrer :

	rails db:migrate

Revert la dernière migration :

	rails db:rollback

Status des migrations :

	rails db:migrate:status
