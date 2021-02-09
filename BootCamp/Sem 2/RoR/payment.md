# Payment
You can not store credit card details on your server (Unless we are PCI compliant)
PCI compliance is not a legislative requirement in Australia but we could face major consequences if there is a data breach and that information is leaked

There are merchants that will handle all of the PCI compliance stuff for us. (They charge but only when used)

- Stripe
- Paypal
- Square
- Eway

## Stripe
www.stripe.com
Very User friendly

#### Setting up Stripe
1. Sign Up
2. Verify your email/sign in
3. Make sure you have a business name inthe top left of your bashboard.
(If you do not click Online events and set one up)
4. Developers -> API Keys
(Public + Secret)

To set up stripe in the rails project, install the stripe gem:
    `bundle add stripe`
Open an editor (nano, vim, code, nvim...) to add the keys encrypted to credentials
    `EDITOR="nvim" rails credentials:edit`

Add the keys to the file (be careful with yml indentation)
```yml
stripe:
  secret_key:{ your secret key }
  public_key:{ your public key }
```
Create a stripe.rb file in `config/initializer` add this line:
`Stripe.api_key = Rails.application.credentials.dig(:stripe, :secret_key)`

---

# Set up Stripe Implementation on Rails
#### Set Up an Online Events App
`rails new online_events -d postgresql`
`cd online_events`
Update values in database.yml
`rails db:create`
`rails g scaffold Event name:string description:string 'price:decimal{7,2}'`
`rails db:migrate`
Create events
Remove "edit" and "destroy options" (optional)
`bundle add stripe`
Set up stripe

#### Create stripe session in the controller
The show action will render the single event and we can add a "buy ticket" button here
That's why we have to create the stripe session in the controller
The session will store which user is going to buy the ticket for which event
All this information must be sent in the session and stripe will connect the created session with our business in our Stripe account


#### In the controller
```ruby
  def show
    session = Stripe::Checkout::Session.create(
      payment_method_types: ['card'],
      customer_email: 'jegoldstein94@gmail.com' # Normally you would get this from the database (current_user.email)
      line_items: [{
        name: @event.name,
        description: @event.description,
        images: ["https://tinyurl.com/yy2qdzjy"], # @event.image
        amount: (@event.price * 100).to_i,
        currency: 'aud',
        quantity: 1 #Can change how many with code
      }],
      payment_intent_data {
        metadata: {
          event_id: @event.id
        }
      },
      success_url: "#{root_url}payments/success?eventId=#{@event.id}",
      cancel_url: "#{root_url}events"
      )
      @session_id = session.id
  end
```

#### Add the "buy" button and the stripe string
We want to render a "buy ticket button"
Also we want to run an event when the button is clicked
This step must be done with JS
We will create a stripe instance (thanks to our keys) and that instance will redirect to the checkout page
The instance will contain the session

```erb
<button data-stripe="payment">Buy ticket <%= number_to_currency(@event.price) %></button>
<%= link_to 'Back' events_path %>
<script src="https://stripe.com/v3/"></script>

<script>
    document.querySelector("[data-stripe='payment']").addEventListener("click", () => {
        const stripe = Stripe("<%= Rails.application.credentials.dig(:stripe, :public_key) %>");
        stripe.redirectToCheckout({
            sessionID: "<%= @session_id %>"
        });
    }):
</script>
```


#### Payments controller and view
In the event controller we said if the checkout was successful we will be redirected to `/payments/success`, so we need that controller and view.
`App/controllers/payments_controller.rb`
```ruby
class PaymentsController <ApplicationController
  def success
  end
end
```
`Apps/views/payments/success.html.erb`
```erb
You've successfully made a payment!
<%= link_to "Go To Events", events_path %>
```

Add the correct routes
```ruby
root "events#index"
  resources :events
  get "/payments/success", to: "payments#success"
```

# THIS DID NOT WORK

# Webhooks

Webhooks are a way for an app to provide other applications with real-time information.
It delivers data to other applications as it happens, meaning you get data immediately.
Stripe has the ability to listen for an internal event and then send a HTTP request to a predefined URL when that event happens.

#### Why do we need a webhook?
We haven't tracked the purchase.
If the user loses internet connection after the payment andw as never redirected to our url we could have issues.
How are we going to verify if the person has truly made a purchase and isn't just faking the data in the url.
This is what a webhook is used for.

## Set up a webhook in stripe

Stripe dashboard -> Developers -> Webhook -> Add endpoint

Stripe is asking us for the destination URL it is going to send this information to, but because the server is running locally we have to fix it with ultrahook

#### What is ultrahook?
It is a gem that provides an internet reachable URL from our computer that then forwards the request on to our localhost.

Visit http://www.ultrahook.com/register and follow the instructions.

#### cont.
Once the gem is installed let's run ultrahook: `ultrahook stripe 3000`

We can go back to Stripe dashboard and add our url to the endpoint.

You can then add the endpoint in stripe, of course we want a new destination that may end in `/payments/webhook`

The events to send would be `checkout.session.completed`

That's it the set up is fully done for those sites

Let's add the webhook route: ultrahook stripe 300
`post "/payments/webhook", to: "payments#webhook"
And the webhook aciton in the payments controller
```ruby
def webhook
  payment_id = params[:data][:object][:payment_intent]
  payment = Stripe::PaymentIntent.retreive(payment_id)
  event_id = payment.metadata.event_id
  #user_id = payment.metadata.user_id
  p "Event Id " + event_id
  #p User Id " + user_id
  render plain: "Success"
end
```
(OF COURSE IT'S FUCKED)

add `skip_before_action :verify_authenticity_token, only: [:webhook]`

