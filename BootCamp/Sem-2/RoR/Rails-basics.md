# Rails Basic

#### Create rails app

To create a rails app you open terminal and type `rails new nameOfApp -d postgresql`
`-d` is the database flag and `postgresql` we will learn later is the database we are using.

*When created it will take a while as it is creating a complete application. The first time is the longest after that it will be much faster.*

This creates a new Directory which is full of files.

#### Folders

Main folders used are:

1. app
2. config
3. db (database)

#### Start Server

To start the rails app you use `rails s` in terminal (It boots up it's own server). The server it uses is puma.

Web servers are how we host the entire web application on the internet.

The default server is on localhost:3000.

To change the server run `rails s -p 3001` (This makes it localhost:3001)

#### Create Database

To create the database we use `rails db:create` again in terminal

