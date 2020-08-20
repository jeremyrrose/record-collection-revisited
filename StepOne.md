# Record Collection Revisited - Step One

From here on out, all instructions pertain to the whole group -- so the first step is to get on the same Git page.

## Group Git

Choose one member of the group to create a new repository on GitHub and a new Rails app with Postgres on their computer by typing `rails new record-collection --database=postgresql --api`. Rails will automatically initialize a Git repository for the project; now `cd` into the project directory and use `git remote add origin <YOUR NEWLY CREATED GIT URI>` to hook it up. Now you can `git push origin master` to your heart's content.

Well, *one* person can... you'll have to add all the group members to the repo on GitHub as contributors. Have another group member test to see if they can clone down the repo, run `bundle install` and `rails db:create`, and fire it up. Neat!

## Basic auth

We know we'll want users to be able to login; you can actually go ahead and set up auth *exactly* like we did in class on Wednesday (though you might want to change the`User` model's `age` field to `email` or something more relevant). That means go through all the steps like enabling the `bcrypt`, `rack-cors`, and `jwt` gems, adding the CORS configuration, putting `has_secure_password` in the `User` model, adding the whole auth chain into `ApplicationController`, and setting up the same user routes and controllers to receive login info and spit out JWTs in return.

Test to make sure the auth system works, then commit the changes and set this aside until later. We've got a lot of other things to set up.

>You may choose to walk through the auth setup as a group *or* designate one person to make the changes while others peek ahead and plan. Either way, you should do it on one computer, then commit and push changes.

## Artist and Record models

Everyone should pull down the auth changes. Now we'll practice Git branching to set up the `Artist` and `Record` models. One person should type `git checkout -b artist-and-record-models` in their terminal... Now they're on a new Git branch! You'll make the next set of changes here.

Our models will have the same shape they had in the Mongoose schemas from before:

| Artist | |
| ----- | ---- |
| name | string|
| hot_100_hits | integer |


| Record | |
| ----- | ----- |
| title | string |
| release_year | integer |
| cover_image | string |
| artist | (artist ID) |

On the new branch, use `rails g model` to create model files and migrations for each, and make sure to define the reference relationships in both model files. (You may also want to add `validates_presence_of` to make sure your models get the right info.) Run `rails db:migrate` and let's see if it worked!

## Seeding

Since you had already typed it out last time, it was easy to convert your data into a seed for Rails. Your code is in [`seed_code.rb`]('seed_code.rb') in this repository. Nice work! You can paste the contents of that file into `db/seeds.rb` and run `rails db:seed`. If you set up your models correctly, you should now be able to use `rails c` to make sure you've got some artists and records in the DB.

>Take a look at the code that actually adds the data. It's pretty simple Ruby with some Rails models, right? You could definitely write something like this next time you need to.

If you're all set, commit the new changes to the `artist-and-record-models` branch. How? If you have the branch checked out, just `git add` and `git commit` as usual. Now type `git push origin artist-and-record-models`... and then head to GitHub to take a look.

Your should now be able to select the new branch on GitHub and submit a pull request to merge it into the master branch. Do that, and click through all the steps. Finally, have one of the other contributors confirm the merge on Github.

Now everyone can type `git pull` in their project repos, and you should all have the updated code. Each person will still need to update their local database, though! Run `rails db:create` if you haven't previously, then run `rails db:reset`. Everyone should now have the database and seed set up locally.

It's time to [set up a few routes and controllers](StepTwo.md).
