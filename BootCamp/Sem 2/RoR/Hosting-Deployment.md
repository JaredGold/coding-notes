# Deployment

Some websites to use are:

Heroku - Free

Digitcal Ocean - good but payed

Amazon EC2 - Costs but free version depending on usage

---

##### READ THE HEROKU GUIDE

You install heroku:

##### On Terrminal *(not completely in order)*:

`heroku login` - login to heroku

`heroku create name` - create a heroku project using name

`heroku git:remote -a name-of-git` - initialise git on heroku 

`git push heroku main` - push to heroku

`heroku open` -  open's heroku website

`heroku logs --tail` - checks logs for errors

`heroku run rails db:migrate` - mirages the database on heroku

`heroku run rails c` local console for heroku database

##### In application.rb file

`config.serve_static_assets = true` - set static images



##### In production.rb file

change `config.assets.compile = true` for static images

