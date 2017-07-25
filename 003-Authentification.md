Authentification
================

On va utiliser la gem [Clearance](https://github.com/thoughtbot/clearance) pour
nous donner de l'authentification.


1. Ouvrez le `Gemfile` et ajoutez cette ligne :

		gem 'clearance'

2. Utilizes Bundler pour installer la gem :

		bundle install

3. Pour installer Clearance, faitez :

		rails generate clearance:install

4. Lancez les migrations :

		rails db:migrate

5. Relancez le serveur Rails

4. Ajoutez cet HTML (copié du README de Clearance) dans le `<body>` du
   `layouts/application.html.erb` :

		<% if signed_in? %>
			<%= current_user.email %>
			<%= button_to "Sign out", sign_out_path, method: :delete %>
		<% else %>
			<%= link_to "Sign in", sign_in_path %>
		<% end %>

4. Inscription et connexion sont maintenant possibles depuis l'interface web de
   l'application.
