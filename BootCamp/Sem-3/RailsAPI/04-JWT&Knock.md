# Rails JWT and Knock

JWT stands for JSON Web Token. The idea of JWT is instead of having the user log in using a cookie that holds a {sessionId} and having the server check to see if the session id is the same we use a token instead. When the user logs in it creates a JWT with a secret the server then sends the JWT back to the browser, after that each request back from the browser to the server the JWT is returned inside of the header. Then the server checks the JWT signature using the secret token to get the user info from that JWT. Fundamentally a JWT is an encoded string with the secret in the server.

Breaking down the JWT it is compromised of 3 parts, the header, payload and verify signature. 

#### Header

The header contains 2 bits of information. The algorithm of encoding and the type. It looks like this:

```json
{
    "alg": "HS256",
    "typ": "JWT"
}
```

 #### Payload

The payload is the section that holds all of the hidden information. It is important to not keep any of the users personal details in this as it can still be broken into to find the users details.

```json
{
    "sub": "1234",
    "name": "John Doe",
    "admin": "true"
}
```

#### Verify Signature

The verify signature is where everything is combined and then the server secret is added

```js
HMACSHA256(
    base64UrlEncode(header) + "." + base64UrlEncode(payload),
    // SECRET
) 
```

---

## How to set up JWT using Knock

The best way to use JWT is using the gem Knock. 

In the Gemfile we first need to uncomment `gem 'bcrypt'` and add `gem 'knock'`. From here we should also use cors by uncommenting `gem 'rack-cors'`. From here we save and then run 
`$ bundle install`

After this if using rails < v6 we need to use `rails g knock:install` (if you do this and run into errors cause you use v6 run `rails d knock:install`)

If using version 6 ruby In the `config > application.rb` we need to change the following line

```ruby
config.load_defaults 6.0 and config.autoloader = :classic
```

Then we can run the above `rails g knock:install` which will create a knock.rb file in the config. We can change things here but we can change the line and uncomment

```ruby
config.token_secret_signature_key = -> {Rails.application.credentials.secret_key_base}
```

Finally in the base controller in the ApplicationController we need to include Knock

```ruby
class ApplicationController < ActionController::API
    include Knock::Authenticatable
end
```



