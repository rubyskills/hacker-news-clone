---
layout: default
title: Setup
---

# Setup 

Head over to the [padrino](http://padrinorb.com) website for the latest and greatest installation instructions. As of writing, the only installation step to get Padrino is to install the gem. Run the following command in your terminal:

     $ gem install padrino

## Creating a New Application

Padrino installed a bin file into your path called padrino. Let's take a look at the options it gives us.

    $ padrino
    Tasks:
      padrino c         # Boots up the Padrino application irb console
      padrino console   # Boots up the Padrino application irb console
      padrino g         # Executes the Padrino generator with given options.
      padrino gen       # Executes the Padrino generator with given options.
      padrino generate  # Executes the Padrino generator with given options.
      padrino help      # Describe available tasks or one specific task
      padrino rake      # Execute rake tasks
      padrino s         # Starts the Padrino application
      padrino start     # Starts the Padrino application
      padrino stop      # Stops the Padrino application
      padrino version   # Show current Padrino Version

    Options:
      -c, [--chdir=CHDIR]            # Change to dir before starting
      -e, --environment=ENVIRONMENT  # Padrino Environment
                                     # Default: development
          [--help]                   # Show help usage

Pretty cool! Right now we're only concerned with creating a new project so we need to look at the generators.

    $ padrino g 
    Please specify generator to use (project, app, mailer, controller, model, migration, plugin)

Running this command returned all of the possible generators you can use. There are two generators that look like what we need to start, project and app. Turns out project is the generator we want to use in the beginning. We'll learn about the app generator later on. Let's check out the project generator's option set.

    $ padrino g project 

    Usage:
      padrino-gen project [name] [options]

    Options:
      -n, [--app=APP]                # The application name
      -b, [--bundle]                 # Run bundle install
      -r, [--root=ROOT]              # The root destination
                                     # Default: .
          [--dev]                    # Use padrino from a git checkout
      -i, [--tiny]                   # Generate tiny app skeleton
      -a, [--adapter=ADAPTER]        # SQL adapter for ORM (sqlite, mysql, mysql2, postgres)
                                     # Default: sqlite
      -p, [--template=TEMPLATE]      # Generate project from template
      -d, [--orm=ORM]                # The database engine component (activerecord, mini_record, datamapper, mongomapper, mongoid, sequel, couchrest, ohm, mongomatic, ripple, none)
       	                             # Default: none
      -t, [--test=TEST]              # The testing framework component (rspec, shoulda, cucumber, bacon, testspec, riot, minitest, none)
                                     # Default: none
      -m, [--mock=MOCK]              # The mocking library component (mocha, rr, none)
                                     # Default: none
      -s, [--script=SCRIPT]          # The javascript library component (jquery, prototype, rightjs, mootools, extcore, dojo, none)
                                     # Default: none
      -e, [--renderer=RENDERER]      # The template engine component (haml, erb, liquid, slim, none)
                                     # Default: haml
      -c, [--stylesheet=STYLESHEET]  # The stylesheet engine component (less, sass, compass, scss, none)
                                     # Default: none

     Description:

	padrino-gen project generates a new Padrino project

That's a lot of options! Padrino is very flexible and let's you choose the libraries you want to use and mix and match to your heart's content. If I'm boring, I can use mysql2 for my adapter, activerecord for my ORM, and erb for my template engine. If I'm a hipster brogrammer, I might opt for mongoid as my ORM, ham for my template engine and sass for my stylesheets. Since I'm boring, let's just use ActiveRecord with the mysql2 adapter, erb and minitest.

     $ padrino g project news -d activerecord -e erb -a mysql2 -t minitest -b

This should show you a list of all the files and directories the project generator created. It then runs bundle install and then prompts you to cd into ./news. Let's do that now:

    $ cd ./news

Now let's start our fresh Padrino application and see it run!

    $ padrino start

Navigate your browser to [localhost:3000](http://localhost:3000) and you should see a blank page. 

Congrats! You're now riding the Padrino.

## Hello Padrino

*NOTE: Assuming you're using git, I would commit your code right now. We'll be resetting the Hello World code example in the next session as it's mainly for demoing purposes. You are also free to skip the next section if you just want to get to the meat and potatos of your hacker news clone app. To cleanup your application after the hello world example (assuming you've already commited), just run git clean -f -d*

OK so our new Padrino application is pretty boring. Let's spice it up a little and earn our Hello Padrino merit badge. 

Let's keep our current server up and running and create a new terminal tab/window to run our next commands. Let's use the controller generator to get up and running quickly.

    $ padrino g controller hello get:world
      create  app/controllers/hello.rb
      create  app/helpers/hello_helper.rb
      create  app/views/hello
       apply  tests/minitest
      create  test/app/controllers/hello_controller_test.rb

You'll notice that the files generated are very similar to rails. You know have a controller, a helper, a hello folder for your views, and a hello controller test. Let's open up the controller and take a peak at what we have.

*app/controllers/hello.rb*

    News.controllers :hello do
      # get :index, :map => "/foo/bar" do
      #   session[:foo] = "bar"
      #   render 'index'
      # end

      # get :sample, :map => "/sample/url", :provides => [:any, :js] do
      #   case content_type
      #     when :js then ...
      #     else ...
      # end

      # get :foo, :with => :id do
      #   "Maps to url '/foo/#{params[:id]}'"
      # end

      # get "/example" do
      #   "Hello world!"
      # end

      get :world do
      end

    end

The comments right after the do block give you a better idea of the power the Padrino routing DSL has to offer. For now, let's delete those comments and just render our world view so it looks like this:

*app/controllers/hello.rb*

    News.controllers :hello do
      get :world do
        render 'hello/world'
      end
    end

The controller generator doesn't create a view for you so we're going to need to create a new erb file for our Hello Padrino! example.

*app/views/hello/world.erb*

    <h1>Hello Padrino!</h1>

Launch your browser again and navigate to [http://localhost:3000/hello/world](http://localhost:3000/hello/world)

Great. We've greated the planet.
