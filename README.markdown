Machinist
=========

Machinist is a Rails plugin to help populate your database with data for tests.

You specify a "blueprint" for each of your models, with reasonable defaults for
the various fields. In your test setup, you use the blueprint to generate data,
overriding any fields you need set for that particular test.

This keeps each of your tests together with the data it depends on, but avoids
cluttering the test with details of all the model fields that aren't relevant
for that test.

If you're familiar with ThoughtBot's factory\_girl, this is similar, but has a
much cleaner syntax.

Example
=======

Create a blueprints.rb file in your test (or spec) directory, and require it
in your test\_helper.rb (or spec\_helper.rb).

    Post.blueprint do
      title "Example Post"
      body  "Lorem ipsum dolor sit amet"
    end
    
    Comment.blueprint do
      post
      author { Faker::Name.name }  # Use the Faker gem to generate a name.
      body   "Lorem ipsum dolor sit amet"
    end

In your tests, you can now do things like:

    # Create a Post in the database.
    @post = Post.make
    
    # Create a Post with a different title.
    @post = Post.make(:title => "A Different Title")
    
    # Create a Comment and a corresponding Post.
    @comment = Comment.make
    
    # Create a Post with several Comments.
    @post = Post.make
    3.times { Comment.make(:post => @post) }
    
Install
=======

    script/plugin install git://github.com/notahat/machinist.git


Copyright (c) 2008 Peter Yandell, released under the MIT license
