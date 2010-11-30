!SLIDE center
![rails_config](rails_config.png)

!SLIDE code
# config.ru - Rack

    @@@ruby
    require File.expand_path(
        '../config/environment',
        __FILE__)
    run Helios::Application

!SLIDE code
# Small Rack App

    @@@ruby
    class HelloWorld
      def call(env)
        [200,
          {"Content-Type" => "text/plain"},
          ["Hello world!"]]
      end
    end

    run HelloWorld

!SLIDE code
# Minimal Rack App

    @@@ruby
    hello_world = lambda  do |env|
      [200,
        {"Content-Type" => "text/plain"},
        ["Hello World!"]]
    end

    run hello_world

!SLIDE
# Middleware

    @@@ruby
    class RackMiddleware
      def initialize(app)
       @app = app
      end

      def call(env)
       # Print the path to stdout
       puts env['PATH']
       @app.call(env)
      end
    end

!SLIDE commandline
# rake middleware

    $ rake middleware
    use Rack::Static
    use ActionDispatch::Static
    use Rack::Lock
    use ActiveSupport::Cache::Strategy::LocalCache
    use Rack::Runtime
    use Rails::Rack::Logger
    use ActionDispatch::ShowExceptions
    use ActionDispatch::RemoteIp
    use Rack::Sendfile
    use ActionDispatch::Callbacks
    use ActiveRecord::ConnectionAdapters::ConnectionManagement
    use ActiveRecord::QueryCache
    use ActionDispatch::Cookies
    use ActionDispatch::Session::CookieStore
    use ActionDispatch::Flash
    use ActionDispatch::ParamsParser
    use Rack::MethodOverride
    use ActionDispatch::Head
    use ActionDispatch::BestStandardsSupport
    use Warden::Manager
    use Sass::Plugin::Rack
    run Helios::Application.routes


