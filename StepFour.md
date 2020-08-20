# Record Collection Revisited - Step Four

Now that we've built relationships between a `User` and the records and artists in their collection, we can build routes and controllers to serve that info. Instead of adding a `PurchasesController` -- we're just using `Purchases` to connect other models, remember? -- we'll add to our `UsersController` and take advantage of the user login capabilities we built earlier.

>![Phil Collins](https://media.giphy.com/media/nqAhSVOPeARZ6/giphy.gif)

>Auth: Members Only

## Getting user-specific info

We'll need these five routes in our front end:

| Request | Route | Controller | Result |
| --- | --- | --- | --- |
| GET | /users/artists | users#user_artists | Return a list of the artists in the logged-in user's collection. |
| GET | /users/records/ | users#user_records | Return a list of the records in the logged-in user's collection. |
| GET | /users/artists/:artist_id | users#user_records_by_artist | Return a list of the records by a *particular* artist in the logged-in user's collection |
| POST | /users/records/:record_id | users#add_record | Create a new `Purchase` connecting the logged-in user to a `Record`. |
| DELETE | /users/records/:record_id | users#remove_record | Delete the `Purchase` connecting the logged-in user to a `Record`. |

We'll build the first method together to show how we can use the new relationships and the login info in tandem.

## Using `before_action`

First, we need to expand our use of the `authorized` method we built in the `ApplicationController`. Find this line near the top of your `UsersController`:

```ruby
    before_action :authorized, only: [:auto_login]
```

And let's add all of our new methods to that array:

```ruby
    before_action :authorized, only: [:auto_login, :user_artists, :user_records, :user_records_by_artist, :add_record, :remove_record]
```

## Getting info from auth

Now `authorized` will be run *before* any of these controllers execute, which means it will pull the info we need from the JWT.

Add this method to your `UsersController`:

```ruby
    def user_artists
        p @user
    end
```

And add this to `config/routes.rb`:

```ruby
    get '/users/artists', to: 'users#user_artists'
```

Make sure your server is running, and go to that route in Postman. (Make sure you're including the 'Authorization' header with a valid user token.) Now look at the log for your server... Looks like you automatically have the logged-in `User` available as `@user`!

Now change your `user_artists` method to this:

```ruby
    def user_artists
        render json: @user.artists
    end
```

Wow, that was easy!

Now assign each of the remaining methods to a member of your group, split up, create branches, and get to work!

Follow the same pattern from Step Two. Once all the controllers are completed and tested and the branches have been merged to the master, your API is all set.

## Deployment

It's a good idea to update the README file inside your Rails project directory with a sentence or two of introduction. You can also include the chart of your routes, which you can find in [resource_chart.md](resource_chart.md).

Now one team member should take the lead in deploying the API to Heroku. Follow the instructions from Thursday morning's lesson... and once it's set, you'll be ready to move on to connecting the front end.
