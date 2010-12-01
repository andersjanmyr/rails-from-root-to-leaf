!SLIDE bullets
# Why Ruby?

* Happiness
* Flexibility
* Lightness
* Glue

!SLIDE code
# Parallel Assignment

    @@@ruby
    # Swap a and b, without a temporary variable
    a, b = b, a

!SLIDE code
# Multiple Return Values

    @@@ruby
    def div(a, b)
      [a/b, a%b]
    end

    a, b = div(5, 2)
    # a = 2, b = 1



!SLIDE code
# String Interpolation

    @@@ruby
    kid = 'Kid'
    "Hello #{kid} ##{1+3}"
    # => Hello Kid #4

!SLIDE code
# Here Documents

    @@@ruby
    sql = <<-SQL
    SELECT allocations.project_id as project_id, year, week, allocations.id as allocation_id
      FROM weeks
      LEFT OUTER JOIN allocations ON allocations.start_date < weeks.end_date
        AND allocations.end_date > weeks.start_date
        AND allocations.project_id = ?
      WHERE weeks.start_date >= ? AND weeks.end_date <= ?
    SQL


!SLIDE code
# Higher Order Functions

    @@@ruby
    # Map converts an array of values to a new array of values
    ["a", "b", "c"].map { |item| item.upcase }
    # => ["A", "B", "C"]

    # Zip zips arrays together
    [1, 2, 3].zip([10, 20, 30])
    # => [[1, 10], [2, 20], [3, 30]]

    # Zip with a function applies the function to the results
    [1, 2, 3].zip([10, 20, 30]) {|arr| arr[0] + arr[1]}
    # => [11, 22, 33]


!SLIDE code
# Simple Commandline Access

    @@@ruby
    # Backticks invokes the command and returns the result as a string
    `ls`
    # => "Scripts\nStylesheets\nbin\nget_destinations.scpt\nlib\nnibs\n"
    `ls`.split
    # => ["Scripts", "Stylesheets", "bin", "get_destinations.scpt", "lib", "nibs"]

    # System invokes the command, prints the result to stdout, and return a boolean
    system('ls -l')
    total 64
    drwxr-xr-x  3 andersjanmyr  admin    102 Aug 29  2009 Scripts
    drwxr-xr-x  3 andersjanmyr  admin    102 Aug 29  2009 Stylesheets
    drwxr-xr-x  5 andersjanmyr  admin    170 Aug 29  2009 bin
    -rw-r--r--  1 andersjanmyr  admin  12312 Aug 29  2009 get_destinations.scpt
    drwxr-xr-x  3 andersjanmyr  admin    102 Aug 29  2009 lib
    drwxr-xr-x  3 andersjanmyr  admin    102 Aug 29  2009 nibs
    # => true

    system('ls tapir')
    ls: tapir: No such file or directory
    # => false


!SLIDE code
# Open Classes

    @@@ruby
    class String
      def vowels
        self.scan(/[aeiouy]/i)
      end
    end

    "A tapir is beautiful".vowels
    # => ["A", "a", "i", "i", "e", "a", "u", "i", "u"]


!SLIDE code
# Class Inheritance

    @@@ruby
    class Mammal
      # This is a class method, that returns all mammals of this kind
      def self.all
        mammals.select do |m|
          m.kind_of? self
        end
      end

      # Another class method that gives access to the class varibable
      def self.mammals
        # @@ is a class variable prefix
        @@all_mammals ||= []
      end

    end

!SLIDE code
# Class Inheritance, cont.

    @@@ruby
    class Tapir < Mammal
    end

    # Add some mammals and a tapir
    Mammal.mammals << Mammal.new << Mammal.new << Tapir.new

    Tapir.all
    # => [#<Tapir:0x000001010fc1a0>]

    Mammal.all
    # => [#<Mammal:0x000001010fc218>, #<Mammal:0x000001010fc1c8>, #<Tapir:0x000001010fc1a0>]

!SLIDE code
# Modules

    @@@ruby


!SLIDE code
# Meta Programming

    @@@ruby
    class Tapir

      [:sniff, :eat].each do |method_name|
        send :define_method, method_name do |thing|
          "I'm #{method_name}ing #{thing}!"
        end
      end

    end


!SLIDE code
# Meta Programming, cont.

    @@@ruby
    t = Tapir.new
    t.eat 'bananas'
    # => I'm eating bananas!

    t.sniff 'glue'
    # => I'm sniffing glue!


!SLIDE code
# Method Missing

    @@@ruby
    # Simple implementation of a Javascript-like structure without inheritance
    class Prototype

      def props
        @props ||= {}
      end

      def method_missing(method, *args)
        m = method.to_s.sub('=', '') # Strip the trailing '=' to allow setters
        if args.empty?
          props[m]
        else
          props[m] = args[0]
        end
      end
    end

!SLIDE code
# Method Missing, cont.

    @@@ruby
    prot = Prototype.new
    prot.age
    # => nil
    prot.age 14
    # => 14
    prot.age
    # => 14
    prot.age= 16
    # => 16
    prot.age
    # => 16




