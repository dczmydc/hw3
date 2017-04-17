# Week 3 - Homework

*5 points*

**DUE: MONDAY, APRIL 24, 12pm noon**

### Overview

Let's rebuild our UChicago Visitor's Guide using real, database-backed models.


### Getting Started

1. Download a ZIP of this repository.  Unzip the contents.
2. In your Terminal or Command Prompt, `cd` to the application's root directory.
3. `bundle install`
4. `rails server`.  Puma should start up on port 3000.
5. Browse to `localhost:3000`.  You should see a Rails welcome page.
6. Browse to `localhost:3000/places`.  You should see some photos of landmarks.
7. Click on any photo.  You should go to a details page.

Your job is to replace these static pages with data-driven, dynamic pages.

### Skills Required
- redirect_to
- routes: `get`, `post`, `patch`, and `delete`
- controller methods
- views
- params hash for dynamic segments
- database-backed models
- seeds
- model CRUD
- `rails db:seed`
- `rails db:migrate`
- HTML forms


### Overview

Your job is to transform this app into a database-backed web application.

1 point per challenge, plus up to 1 point for overall code readability (good variable names, consistent indentation, etc.).

### Challange #1: A `Place` Model

By the end of this challenge, you should have 2 routes like this:

``` ruby
  root 'places#index'
  get '/places' => 'places#index'
```

1. Create a model named Place that can keep track of each place's title, photo, and description.  The title can be limited to 255 characters, but the description shoud support text at least 1000 characters in length.  The admission price should be stored as integer representing the number of cents.
1. Write code in your `db/seeds.rb` file so that it is prefills the database with at least 3 places.  Make sure that you can run the seeds file multiple times and still end up with the same number of places each time.
1. Implement your `index` view to show a nice list of places to visit. (Need some UI inspiration?  Use the static mockups provided in `hw2`.)


### Challenge #2: Let Users View Details

By the end of this challenge, you should have 3 routes like this, but _not necessarily in this order_:

``` ruby
  root 'places#index'
  get '/places' => 'places#index'
  get '/places/:id' => 'places#show'
```

1. Support the following url: `/places/:id` and connect it to an action method named `show` in the `PlacesController`.  This action should display all of the details of a particular Place.
1. Modify the `index` action so that clicking on a place links to the `show` page for that place.
3. Both the `index` and `show` pages should display a common header at the top of the page.  Something in the header should also act as a link to the home page. Feel free to be creative: we're building a visitor's tour guide for the university!

### Challenge #3: Delete Places

By the end of this challenge, you should have 4 routes like this, but _not necessarily in this order_:

``` ruby
  root 'places#index'
  get '/places' => 'places#index'
  get '/places/:id' => 'places#show'
  delete '/places/:id/delete' => 'places#delete'
```

1. On the `index` page, add a link next to each place that will trigger the `places#delete` action.
2. When the user clicks the link, that Place should be removed from the database, and the user should be redirected back to the `index` page to verify that the place has been removed.

### Challenge #4: Add and Edit Places

By the end of this challenge, you should have these 8 routes, but **not necessarily in this order**:

``` ruby
  root 'places#index'
  get '/places' => 'places#index'
  get '/places/:id' => 'places#show'
  delete '/places/:id' => 'places#delete'
  get '/places/new' => 'places#new'
  post '/places' => 'places#create'
  get '/places/:id/edit' => 'places#edit'
  patch '/places/:id' => 'places#update'
```

1. At the top of the index page, add a link to add a new place.  The link should navigate to `/places/new`, which must display a form for the user to fill in (title, url, price, and a description).
1. The form should target the `create` action. When the user submits the form, a new row should be added to the database, and the user should be redirected back to the `index` action to see a refreshed list that now includes their new place.
1. On the `show` page, add a link to `/places/:id/edit` which should display a form to edit the details of the place.
1. The edit form should be prefilled with data from the database, and it should trigger the `update` action when the suer clicks Submit.
1. The `update` action should update the row in the database, and redirect to `/places/:id` so the user can verify that the database has been updated.



### HINTS

* Research the `text_area_tag` to allow for multiline input fields.
* If something isn't working and you can't figure out why, watch the **server log**.

Here are some Rails view helper methods that you might find helpful:

* [`link_to`](http://api.rubyonrails.org/classes/ActionView/Helpers/UrlHelper.html#method-i-link_to)
* [`image_tag`](http://api.rubyonrails.org/classes/ActionView/Helpers/AssetTagHelper.html#method-i-image_tag)
* [`simple_format`](http://api.rubyonrails.org/classes/ActionView/Helpers/TextHelper.html#method-i-simple_format)
* [`text_field_tag`](http://api.rubyonrails.org/classes/ActionView/Helpers/FormTagHelper.html#method-i-text_field_tag)
* [`submit_tag`](http://api.rubyonrails.org/classes/ActionView/Helpers/FormTagHelper.html#method-i-submit_tag)
* [`number_to_currency`](http://api.rubyonrails.org/classes/ActionView/Helpers/NumberHelper.html#method-i-number_to_currency)

FRIENDLY WARNING: Contrary to what you may read online, do NOT use `form_for` (at least, not this week).  You can build everything you need with `form_tag` and `link_to`.

And here are some command-line utilities that are helpful:

* `rails db:migrate`
* `rails db:seed`
