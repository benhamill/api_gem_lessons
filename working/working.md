!SLIDE subsection
# Things to keep an eye on as you go.

!SLIDE
###### Separate business logic from API access.
## Cleaner logic. Better tests.

!SLIDE bullets
###### API Access

* HTTP
* Authentication
* Caching
* URL Building

!SLIDE
###### Dependency Injection

!SLIDE
    @@@ruby
    describe Meeting do
      let(:api) { double(:api) }
      subject { Meeting.new(api) }

      describe "#go" do
        it "hits the API" do
          api.should_receive(:get).
            with(whatever: 'args')

          subject.go
        end
      end
    end

!SLIDE
###### "Waste" time making a DSL

!SLIDE
    @@@ruby
    class Meeting
      extend MyGem::API::Resource

      has_many :attendees

      primary_key :id

      deletable
      fetchable
    end

!SLIDE
###### `rake console`
## Using `pry`.

!SLIDE
    @@@ruby
    task :console do
      require 'pry'
      require File.expand_path(
        File.dirname(__FILE__) +
        '/lib/my_gem'
      )

      # Interesting stuff here.

      Pry.start
    end

!SLIDE
    @@@ruby
    task :console do
      #...

      config = ...
      @api = MyGem.new(
        config['key'],
        config['secret']
      )

      #...
      Pry.start
    end

!SLIDE
    @@@ruby
    task :console do
      #...

      def reload
        reload_msg = 'Reloading...'
        puts reload_msg
        Pry.save_history
        exec('rake console')
      end

      #...
      Pry.start
    end

!SLIDE
    @@@ruby
    task :console do
      #...

      welcome = <<-EOS
        Sup? Check out @api.
      EOS

      puts welcome
      Pry.start
    end

!SLIDE bullets incremental
###### Documentation

* YARD, RDoc, anything!
* RubyDoc.info
* Code
* Existing API docs

!SLIDE
###### `README.md`
