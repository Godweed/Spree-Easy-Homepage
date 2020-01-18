# SpreeEasyHomepage

This is a complete open source [Spree](https://github.com/spree/spree) extension for easily managing your website's homepage products. Particularly useful for programmers who have clients or users with limited technological literacy. The current default operation for managing your homepage is cubersome and time consuming for what is suppose to be a simple operation. Spree also does not include related frontend helpers which would require effort from the programmer to create and maintain.

![SpreeEasyHomepage Demonstration](https://media.giphy.com/media/ekedAYQFgW0iIW1hCg/giphy.gif)

**SpreeEasyHomepage** provides a beautiful and intuitive interface for populating and categorizing products without comprimising ease of use. Developers would be delighted to know that setup is as simple as calling a single method from the view.


Getting Started
----------------------

##### Add this extension to your Gemfile with this line:

```ruby
gem 'spree_easy_homepage'
```

##### Install the gem

```shell
bundle install
```

##### Run the install generators from your console

```shell
rails g spree_easy_homepage:install
```

Admins can manage their Homepage by navigating to the configurations tab from the sidebar.

Frontend Setup
----------------------

#### To populate your homepage with products

Expose this gem's frontend helper in your controller, eg:

```ruby
class ApplicationController < ActionController::Base
  helper Spree::EasyHomepageHelper
end
```
Then from your view, add the helper method `fill_with_sections` eg:

```
<div class="row">
  <%= fill_with_sections %>
</div>
```

#### Thats it!

`fill_with_sections` defaults to use the product "tile" partial in `app/views/spree/products/_product.html.erb`. If none are found in your project folder, the call is delegated to the official "tile" partial used by Spree.

The default product "tile" partial can be optionally overriden by passing `locals: {product_partial: '/path/to/tile_partial'}` in `fill_with_sections` arguments. EG:

```ruby
fill_with_sections(locals: {product_partial: 'spree/shared/product_tile'})
```

If you want to pass variables to the product "tile" partial, you can use `product_locals: {}`, similar to the procedure above. EG:

```ruby
fill_with_sections(locals: {product_locals: {taxon: @taxon, product_tile_size: :small}})
```

deep inside the helper, between the products loop, the locals passed from the above code is passed to the product "tile" partial:

```ruby
render partial: 'spree/products/product', locals: {product: product, taxon: @taxon, product_tile_size: :small}
```

Information
----------------------

#### Editing the view generated by `fill_with_sections`

By default, `fill_with_sections` renders the `_home_sections.html.erb` partial located in `app/views/spree/shared/`. To change the default path.

```ruby
fill_with_sections(partial: 'spree/shared/custom_home_sections')
```

or simply create a `_home_sections.html.erb` partial file in your `spree/shared` folder.

If you want to edit the HTML elements outputted by `fill_with_sections`. Investigate the `shared/_home_sections.html.erb` partial from the gem then override with your edited version in your main project as instructed above.

Testing via Rspec
----------------------

From the gem's root folder

```shell
bundle install
```

Generate a dummy app via Rspec

```shell
bundle exec rake generate_dummy_app
```

Then call Rspec

```shell
rspec
```

Note: for feature tests, chrome (headless) is selected by default.


##### Run the install generators from your console

```shell
rails g spree_easy_homepage:install
```

Contributing
----------------------
This gem has been released only recently. Feedback is appreciated. I have no guidelines for pull-requests other than the basic description and reproduction steps (for bugs). Proper OOP must be followed for feature submissions.

Copyright (c) 2020 [Jibril Tapiador](https://www.jibril.ch/), released under the New BSD License.
