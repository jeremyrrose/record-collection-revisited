# Record Collection Revisited - Step Three

Your uncle's *copy* of Cyndi Lauper's *She's So Unusual* belongs to him, sure. 

But that masterpiece *belongs to the world.* Well, or... in our database model anyway, it `belongs_to` the `Artist`. So how can we let your uncle add it to his collection?

>![Oh, Cyndi!](https://media.giphy.com/media/kFFWGnCJWE1hu/giphy.gif)

>True colors, shining `through:`

## Many to many, through

We want to enable each of our app's users to `have_many` records, and we want to enable each record to `have_many` satisfied listeners. This is called a "many-to-many" relationship. Very progressive!

But we can't just start plopping IDs into an array like we might in MongoDB and call it a day. SQL databases aren't really built to handle arrays, so the easiest way to achieve our goal in Rails is by creating a new model that just handles the connection between a `User` and a `Record`.

We'll call the new model a `Purchase` (for lack of a better term). Literally all each purchase needs to do is hold a `User` ID and a `Record` ID. So one member of your group can do `rails g model Purchase users:references records:references` and *voila!* there's now a way for your uncle to stake his claim to *Like A Prayer* even though it `belongs_to` Madonna.

We still need to add the relationships to the models, though. Both `Record` and `User` will have a `has_many :purchases`, and each of them will `have_many` of the other `through: :purchases`. 

Let's go one step further and let each `User` have a list of artists whose records they own. Add the following to the `User` model:
```ruby
    has_many :artists, -> { distinct }, through: :records
```

>The lambda function here (`-> { distinct }`) ensures that the list will only include unique `Artist` entries. Your uncle has a lot of records, true, but there's only *one* Madonna.

Once everything is set up, test out the new model in the Rails console. Now push the changes to the master and have everyone pull!

>Don't forget that `git pull` will change the *code* in your repository... but it won't change your database structure until you run `rails db:migrate` or `rails db:reset`.

If anyone is having trouble understanding what just happened, pause and talk it through until everyone in the gets it. Once everyone's on the same page, let's [write just a few more controllers](StepFour.md).
