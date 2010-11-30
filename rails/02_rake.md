!SLIDE
# Rake, Ruby Make

!SLIDE code
# Rake Task

    @@@ruby
    # Rakefile

    desc "Says hello"
    task :hello do
        puts 'hello'
    end

    desc "Says goodbye"
    task :goodbye => :hello do
        puts 'goodbye'
    end

!SLIDE commandline
# rake -T  # show tasks

    $ rake -T
    (in /Users/andersjanmyr/Desktop)
    rake goodbye  # Says goodbye
    rake hello    # Says hello

!SLIDE commandline incremental
# rake # invoke rake

    $ rake hello
    hello
    $ rake goodbye
    hello
    goodbye



!SLIDE commandline
# Rake in Rails

    $ rake -T
    rake db:create        # Create the database from config/database.yml for...
    rake db:migrate       # Migrate the database (options: VERSION=x, VERBOS...
    rake db:rollback      # Rolls the schema back to the previous version (s...
    rake db:seed          # Load the seed data from db/seeds.rb
    rake db:setup         # Create the database, load the schema, and
    rake diagram:all      # Generates all SVG class diagrams.
    rake doc:app          # Generate docs for the app -- also availble doc:r...
    rake hudson:rcov      # Run all specs with rcov
    rake log:clear        # Truncates all *.log files in log/ to zero bytes
    rake middleware       # Prints out your Rack middleware stack
    rake notes            # Enumerate all annotations (use notes:optimize,
    rake routes           # Print out all defined routes in match order,
    rake spec             # Run all specs in spec directory (excluding plugi...
    rake stats            # Report code statistics (KLOCs, etc) from the app...
    rake test             # Runs test:units, test:functionals, test:integrat...
    rake time:zones:all   # Displays all time zones, also available: time:zo...
    rake tmp:clear        # Clear session, cache, and socket files from tmp/...
    rake tmp:create       # Creates tmp directories for sessions, cache, soc...


