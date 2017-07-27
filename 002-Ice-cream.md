Ice cream
=========

1. Ajoutez un modèle pour nos glaces :

		rails g model ice_cream flavor:string manufacturer:string

2. Lancez les migrations :

		rails db:migrate

2. Créez une nouvelle glace dans la console Rails :

		$ rails c
		> IceCream.create(flavor: 'Vanille', manufacturer: 'Picard')

	Sortez de la console avec Control-D

3. Créez un controller pour nos glaces :

		rails g controller ice_creams index --skip-routes

4. Ajouter une route index. Ouvrez `config/routes.rb` et écrivez :

		root 'ice_creams#index'

5. Dans un nouveau terminal, lancez le serveur de développement Rails :

		rails s

	Naviguez à `http://localhost:3000`, et vous devrez voir un placeholder pour
	la page index des glaces.

6. Ouvrez notre controller (`app/controllers/ice_creams_controller.rb`) et
   ajoutez cette ligne à la méthode `index` :

		@ice_creams = IceCream.all

	Les variables d'instance, précédées par des `@`, sont accessibles dans les
	templates.

7. Ouvrez notre template index (`app/views/ice_creams/index.html.erb`).
   Remplacez le contenu avec :

		<% if @ice_creams.present? %>
			<ul>
				<% @ice_creams.each do |ic| %>
					<li>
						<%= ic.flavor %>, <%= ic.manufacturer %>
					</li>
				<% end %>
			</ul>
		<% end %>

8. Rechargez la page dans votre navigateur. Vous devrez voir la glace que nous
   avons crées avant affiché sur la page.

9. Ouvrez le layout (`app/views/layouts/application.html.erb`), et ajoutez cette
   ligne au-dessus du `<%= yield %>` :

		<h1>Deux Scoops</h1>

	Quand vous rechargez la page, un header devrait apparaître au-dessus de la
	liste de glaces. L'HTML dans le template layout est rendu sur tous les pages
	de l'application.
