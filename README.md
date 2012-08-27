
Do the following to get this working...
==Install ElasticSearch==
On Mac - use homebrew
brew install elasticsearch
  elasticsearch -f -D es.config=/usr/local/Cellar/elasticsearch/0.18.5/config/elasticsearch.yml

==On Windows==
Grab the installer here...
https://github.com/rgl/elasticsearch-setup/downloads

you must restart your computer on windows...
Access here to make sure it is working after the restart...
http://localhost:9200/

==Then run the following commands...==

  bundle
  rake db:setup
  start your server

Requires Ruby 1.9.2 or later to run.

== For the most basic usage of elasticsearch do the following==

controller....add code...
Article.search(params)

model....
  include Tire::Model::Search
  include Tire::Model::Callbacks
  
  def self.search(params)
    tire.search(load: true) do
      query { string params[:query], default_operator: "AND" } if params[:query].present?
    end
  end
  
  view...
  <%= form_tag articles_path, method: :get do %>
  <p>
    <%= text_field_tag :query, params[:query] %>
    <%= submit_tag "Search", name: nil %>
  </p>
<% end %>