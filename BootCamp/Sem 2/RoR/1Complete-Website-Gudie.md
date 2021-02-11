# Car Sales
1. Create a car rails project `rails new car -d --postgresql -T` Don't quote me on that
2. Add rails-rspec to gemfile `gem rspec-rails`
3. Create db
4. run `rails g rspec:install`
5. If rspec is not installed you can run `bundle exec rspec` and it runs it through the project
6. Generate a scaffold `rails g scaffold Listing title description:text price:integer sold:boolean`

## Set up Heroku for deployment
- `heroku login`
- `heroku create name`
- `git push heroku main`
