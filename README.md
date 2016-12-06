# Steps

1. rails new my-project
1. go to `app/views/layouts/application.html.erb`
  * remove turbolinks references
  * move javascript inclusion to bottom of body and add `async: true` option to it
1. remove gems from Gemfile you won't use (jquery, turbolinks etc)
1. add `gem 'browserify-rails'` to Gemfile
1. `$ bundle install`
1. `$ npm init -y`
1. `$ npm i browserify browserify-incremental react react-dom`
1. `$ npm i -D babelify babel-preset-es2015 babel-preset-react`
1. add this to your `package.json`
   ```js
   "browserify": {
     "transform": [
       "babelify"
     ]
   }
   ```
1. create a `.babelrc` file at your project root
   ```
   {
     "presets": ["es2015", "react"]
   }
   ```
1. alter `app/assets/javascripts/application.js` to be nothing more than
   ```js
   //= require cable
   require('browser')
   ```
1. create a file in that same JS directory named `browser.js` (or whatever you want) and fill it with
   ```js
   import React from 'react'
   import ReactDOM from 'react-dom'
   import App from './App'

   const div = document.createElement('div')
   document.body.appendChild(div)
   ReactDOM.render(<App />, div)
   ```
1. create the App component file, `App.js`
   ```js
   import React, { Component } from 'react'

   export default class App extends Component {
     render() {
       return (
         <div>Hello world!</div>
       )
     }
   }
   ```
1. Create a default root at `config/routes.rb`
   ```rb
   root to: 'home#index'
   ```
1. create a `HomeController` with a method named `index`
1. create `app/views/home/index.html.erb`
1. Create your application db:
   ```
   $ rails db:create db:migrate
   ```
1. start your server
   ```
   $ rails s
   ```
1. navigate to `localhost:3000` and see it working

This is a relatively easy set up for getting React + Babel running in your Rails app and still preserve access to ActionCable.
