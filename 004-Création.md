Création
========

On va ajouter un formulaire pour créer une nouvelle glace.


1. Lancez cette commande :

		rails routes

	La commande affiche toutes les routes/URLs dans notre application, avec les
	noms que Rails utilise pour ses helpers dans la première colonne, et les
	mappings des controllers dans la dernière colonne.

2. Ajoutez cette ligne à `config/routes.rb` :

		resources :ice_creams

	Ça va nous créer des routes RESTful pour le controller
	`IceCreamsController`. Relancez `rails routes` pour voir la différence.

3. Ajoutez une méthode `new` dans notre controller :

		def new
		  @ice_cream = IceCream.new
		end

4. Créez un template correspondant à cette méthode dans
   `app/views/ice_creams/new.html.erb`, et remplissez-le avec ce formulaire :

		<%= form_with model: @ice_cream do |f| %>
			<div>
				<%= f.label :flavor %>
				<%= f.text_field :flavor, id: :ice_cream_flavor %>
			</div>

			<div>
				<%= f.label :manufacturer %>
				<%= f.text_field :manufacturer, id: :ice_cream_manufacturer %>
			</div>

			<div>
				<%= f.submit %>
			</div>
		<% end %>

5. Ajoutez une méthode au controller pour capter les paramètres venant du
   formulaire :

		private

		def ice_cream_params
		  params.require(:ice_cream).permit(:flavor, :manufacturer)
		end

	(http://guides.rubyonrails.org/action_controller_overview.html#strong-parameters)

6. Ajoutez une méthode `create` au controller :

		def create
		  @ice_cream = IceCream.new(ice_cream_params)

		  if @ice_cream.save
		    redirect_to ice_creams_path
		  else
		    render :new
		  end
		end

	On essaye de sauvegarder la glace venant du formulaire. Si on réussi, on
	redirect à la page index du `IceCreamsController`, sinon on affiche le
	formulaire.

7. Pour l'instant, nos glaces ne sont pas associés à un utilisateur. On va faire
   ça maintenant. D'abord, on va assurer que les utilisateurs sont authentiqués
   avant de changer une glace. Ajoutez cette ligne au début de la classe
   `IceCreamsController` :

		before_action :require_login, except: [:index, :show]

8. Maintenant, on va créer une association dans la base de données entre nos
   glaces et nos utilisateurs :

		rails g migration add_user_id_to_ice_creams user:references

9. `rails db:migrate`

10. On va ajouter des associations entre les modèles `User` et `IceCream`.
	Mettez ces lignes dans les classes des modèles :

		# app/models/ice_cream.rb
		belongs_to :user

		# app/models/user.rb
		has_many :ice_creams

11. Dans `IceCreamsController#create`, on va associer la nouvelle glace avec
	l'utilisateur connecté :

		# Remplacez
		@ice_cream = IceCream.new(ice_cream_params)
		# par
		@ice_cream = current_user.ice_creams.build(ice_cream_params)

	Maintenant, quand on crée des glaces en passant par le formulaire, ces
	records seront associés avec notre utilisateur.
