# Record Collection Revisited - Step Three

Your uncle's *copy* of Cyndi Lauper's *She's So Unusual* belongs to him, sure. But that masterpiece *belongs to the world.* Well, or... in our database model anyway, it `belongs_to` the `Artist`. So how can we let your uncle add it to his collection?

## Many to many, through

We want to enable each of our app's users to `have_many` records, and we want to enable each record to `have_many` satisfied listeners. This is called a "many-to-many" relationship. Very progressive!

But we can't just start plopping IDs into an array like we might in MongoDB and call it a day. SQL databases aren't really built to handle arrays, so the easiest way to achieve our goal in Rails is by creating a new model that just handles the connection between a `User` and a `Record`.

We'll call the new model a `Purchase` (for lack of a better term). Literally all each purchase needs to do is hold a `User` ID and a `Record` ID. So one member of your group can do `rails g model Purchase users:references records:references` and *voila!* there's now a way for your uncle to stake his claim to "Like A Prayer" even though it `belongs_to` Madonna.

We still need to add the relationships to the models, though. Both `Record` and `User` will have a `has_many :purchases`, and each of them will `have_many` of the other `through: :purchases`. Once this is set up, push the changes to the master and have everyone pull.

>Don't forget that `git pull` will change the *code* in your repository... but it won't change your database structure until you run `rails db:migrate` or `rails db:reset`.

