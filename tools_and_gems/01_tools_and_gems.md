!SLIDE
# Tools

!SLIDE
# RVM
## Ruby Version Manager

!SLIDE
# Livereload

!SLIDE code
# terminitor

    @@@ruby
    tab "LiveReload" do
      tab_name("Livereload")
      run "rvm use system"
      run "livereload"
    end

    tab "Rails" do
      tab_name("Rails")
      run "rails server"
    end

    tab "Bash" do
      run "cd ~/projects/helios"
    end

!SLIDE
# autotest

!SLIDE
# Spork

!SLIDE code
# Watchr

    @@@ruby
    watch('test/test_helper\.rb') { run_all_tests }
    watch('test/.*/.*_test\.rb') { |m| run_test_file(m[0]) }
    watch('app/.*/.*\.rb') do |m|
        related_test_files(m[0]).map do|tf| run_test_file(tf) }
    end
    watch('features/.*/.*\.feature') { run_all_features }

!SLIDE
# Capistrano

    @@@sh
    cap deploy               # Deploys your project.
    cap deploy:migrations    # Deploy and run pending migrations.
    ...
    cap deploy:rollback      # Rolls back to a previous version and restarts.
    cap deploy:setup         # Prepares one or more servers for deployment.
    cap deploy:start         # Start the application servers.
    cap deploy:stop          # Stop the application servers.
    cap invoke               # Invoke a single command on the remote servers.
    cap shell

!SLIDE
# God

    @@@ruby
    God.watch do |w|
        w.name = "gravatar2-mongrel-#{port}"
        w.interval = 30.seconds # default
        w.start = "mongrel_rails start -c #{RAILS_ROOT} -p #{port} \
          -P #{RAILS_ROOT}/log/mongrel.#{port}.pid  -d"
        w.stop = "mongrel_rails stop -P #{RAILS_ROOT}/log/mongrel.#{port}.pid"
        w.restart = "mongrel_rails restart -P #{RAILS_ROOT}/log/mongrel.#{port}.pid"
        w.start_grace = 10.seconds
        w.restart_grace = 10.seconds
        w.pid_file = File.join(RAILS_ROOT, "log/mongrel.#{port}.pid")

        ...
     end


!SLIDE
# Gems
## http://www.ruby-toolbox.com/

!SLIDE code
# Sintra (web service framework)

    @@@ruby
    require 'sinatra'

    get '/hi' do
      "Hello World!"
    end

!SLIDE code
# Sass (view)

    @@@css

!SLIDE code
# Haml (view)

    @@@python

!SLIDE code
# SimpleForm (view)

    @@@ruby

!SLIDE code
# Formtastic (view)

    @@@python
    <% semantic_form_for @post do |form| %>
       <%= form.inputs :title, :body, :created_at %>
       <% form.semantic_fields_for :author do |author| %>
         <%= author.inputs :first_name, :last_name, :name => "Author" %>
       <% end %>
       <%= form.buttons %>
     <% end %>
     <% end %>



!SLIDE code
# will_paginate (view)

    @@@ruby
    class Post < ActiveRecord::Base
      cattr_reader :per_page
      @@per_page = 10
    end

    #controller
    @posts = Post.paginate :page => params[:page], :order => 'created_at DESC'

    #view
    <%= will_paginate @posts %>

!SLIDE code
# InheritedResouces (controller)

    @@@ruby

!SLIDE code
# Responder (controller)

    @@@ruby

!SLIDE code
# acts_as_taggable (model)

    @@@ruby
    class User < ActiveRecord::Base
      # Alias for <tt>acts_as_taggable_on :tags</tt>:
      acts_as_taggable
    end

    @user = User.new(:name => "Bobby")
    @user.tag_list = "awesome, slick, hefty"

    # Usage
    User.tagged_with("awesome").by_date


!SLIDE code
# mongoid (model)

    @@@ruby

!SLIDE code
# paperclip (model)

    @@@ruby
    class User < ActiveRecord::Base
        has_attached_file :avatar,
            :styles => { :thumb => "100x100>" }
    end

    #form
    = simple_form_for(@item,
        :html => { :multipart => true }) do |f|
      .inputs
        = f.file_field :attachment

    #show
    = image_tag @item.attachment.url(:thumb)


!SLIDE code
# devise (authentication)

    @@@ruby
    # routes.rb
    devise_for :users

    # new_user_session GET    /users/sign_in(.:format)            {:action=>"new", :controller=>"devise/sessions"}
    # user_session POST   /users/sign_in(.:format)            {:action=>"create", :controller=>"devise/sessions"}
    # destroy_user_session GET    /uses/sign_out(.:format)           {:action=>"destroy", :controller=>"devise/sessions"}

    class User < ActiveRecord::Base
      devise :database_authenticatable, :recoverable,
        :rememberable, :trackable, :validatable



!SLIDE code
# omniauth (authentication)

    @@@ruby
    # config/initializer/omniauth.rb
    Rails.application.config.middleware.use OmniAuth::Builder do
      provider :twitter, ENV['TWITTER_CONSUMER_KEY'],
        ENV['TWITTER_CONSUMER_SECRET']
    end

    # routes.rb
    match '/auth/:provider/callback', :to => 'sessions#create'


!SLIDE code
# rspec (test)

    @@@ruby


!SLIDE code
# cucumber (test)

    @@@python
    Feature: Search courses
      In order to ensure better utilization of courses
      Potential students should be able to search for courses

      Scenario: Search by topic
        Given there are 240 courses which do not have the topic "biology"
        And there are 2 courses A001, B205 that each have "biology" as one of the topics
        When I search for "biology"
        Then I should see the following courses:
          | Course code |
          | A001        |
          | B205        |


!SLIDE code
# factory_girl (test)

    @@@ruby
    Factory.define :item do |f|
      f.title "A title"
      f.desc "A description"
    end

    # Usage
    factory = Factory(:item)

!SLIDE code
# ruby-debug (dev)

    @@@ruby


!SLIDE code
# irbtools (irb)

    @@@ruby
    * wirble colorize output
    * fancy_irbt put result as comment and more colorization
    * hirb (active record) tables and custom views for specific objects
    * fileutils cd, pwd, ln_s, mv, rm, mkdir, touch … ;)
    * ap nice debug printing (ap)
    * yaml nice debug printing (y)
    * clipboard easy clipboard access (copy & paste)
    * guessmethod automatically corrects typos (method_missing hook)








