OAuth2Provider
==============

OAuth 2 Provider example with step by step implementation. The base project is a Rails-API application but the same steps apply for standard Rails. It uses Doorkeeper for the oauth provider implementation.

## Install

1. Add Doorkeeper to your Gemfile: `gem 'doorkeeper'`
2. Run installer generator: `rails generate doorkeeper:install`
3. Generate migrations: `rails generate doorkeeper:migration`
4. Migrate: `rake db:migrate`

## Verify

### Database

We’re using PostgreSQL in this example. The list of relations should look list this (for a brand new project):

```plain
                      List of relations
 Schema |            Name            |   Type   |    Owner
--------+----------------------------+----------+-------------
 public | oauth_access_grants        | table    | jboursiquot
 public | oauth_access_grants_id_seq | sequence | jboursiquot
 public | oauth_access_tokens        | table    | jboursiquot
 public | oauth_access_tokens_id_seq | sequence | jboursiquot
 public | oauth_applications         | table    | jboursiquot
 public | oauth_applications_id_seq  | sequence | jboursiquot
 public | schema_migrations          | table    | jboursiquot
```

### Routes

`rake routes` should yield the following:

```plain
                       Prefix Verb   URI Pattern                                  Controller#Action
                              GET    /oauth/authorize/:code(.:format)             doorkeeper/authorizations#show
          oauth_authorization GET    /oauth/authorize(.:format)                   doorkeeper/authorizations#new
                              POST   /oauth/authorize(.:format)                   doorkeeper/authorizations#create
                              PATCH  /oauth/authorize(.:format)                   doorkeeper/authorizations#update
                              PUT    /oauth/authorize(.:format)                   doorkeeper/authorizations#update
                              DELETE /oauth/authorize(.:format)                   doorkeeper/authorizations#destroy
                  oauth_token POST   /oauth/token(.:format)                       doorkeeper/tokens#create
                 oauth_revoke POST   /oauth/revoke(.:format)                      doorkeeper/tokens#revoke
           oauth_applications GET    /oauth/applications(.:format)                doorkeeper/applications#index
                              POST   /oauth/applications(.:format)                doorkeeper/applications#create
        new_oauth_application GET    /oauth/applications/new(.:format)            doorkeeper/applications#new
       edit_oauth_application GET    /oauth/applications/:id/edit(.:format)       doorkeeper/applications#edit
            oauth_application GET    /oauth/applications/:id(.:format)            doorkeeper/applications#show
                              PATCH  /oauth/applications/:id(.:format)            doorkeeper/applications#update
                              PUT    /oauth/applications/:id(.:format)            doorkeeper/applications#update
                              DELETE /oauth/applications/:id(.:format)            doorkeeper/applications#destroy
oauth_authorized_applications GET    /oauth/authorized_applications(.:format)     doorkeeper/authorized_applications#index
 oauth_authorized_application DELETE /oauth/authorized_applications/:id(.:format) doorkeeper/authorized_applications#destroy
             oauth_token_info GET    /oauth/token/info(.:format)                  doorkeeper/token_info#show
```

### Initializer

Ensure you have the following files: 

* `config/initializers/doorkeeper.rb`
* `config/locales/doorkeeper.en.yml`