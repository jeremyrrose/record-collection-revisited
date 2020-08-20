# Record Collection Revisited - Step Two

Next we'll create controllers for `:artists` and `:records`. Have one member of the group run `rails g controller Artists` and `rails g controller Records`, commit changes, and push up to the master branch. Now everyone can do `git pull` to get up to date.

## Endpoints

We'll only need certain endpoints for the front end of the app:

| Request | Route | Controller | Result |
| --- | --- | --- | --- |
| GET | /artists/:artist_id | artists#show | Return a single artist *including* that artist's records. |
| POST | /artists/ | artists#create | Create an artist. |
| POST | /artists/:artist_id/records | records#create | Create a new record for the given :artist_id. |
| GET | /artists/search/:search_string | artists#search | Return a list of artists that match the search string. |

>Wait... *search*? You can do it. Rails' `.where()` model method lets you pass in an SQL query string, and you know that SQL's `LIKE` plus the `%` wildcard lets you look for partial matches. Right? Mess around with it in the Rails console until a search string of "ryl Ha" helps you find the entry for "Darryl Hall & John Oates".

>If you need to *include* a related model in your JSON response, Rails makes it easy for you with the `include:` keyword.

## Reverse Voltron! (Time to split up)

Let's practice Git a bit. Assign one member of the group to write each controller and add the necessary route. Once you have your assignment, type `git checkout -b my-branch-name` where `my-branch-name` is a descriptive name for the branch *you* are working on (like `artist-search` or the like).

Now you can fiddle around with your controller all you want and it won't affect the master branch until you tell it to! Once your controller is finished and tested, commit your changes, type `git push origin my-branch-name`, and submit a pull request on GitHub to merge your changes into the master.

>You can test *other* people's branches before merging by doing `git pull` and then checking out the branch with `git checkout the-branch-name` (do *NOT* include the `-b` flag here). You can switch back to your branch at any time by typing `git checkout my-branch-name`.

## Reverse Reverse Voltron!

Decide as a team how you want to merge changes. You could merge each controller method to the master as it is completed, or wait until they're all done and merge one by one at that point. Once the merge is done, everyone should `git pull` so that each person has the current master on their machine. Now do `git checkout master` to switch back to the master and test everything together!

>Make sure to check out your teammates' code. If you see something you think should change, speak up! If there's something you don't understand, ask!

>Each team member will probably have different junk in their local database at this point. This may not necessarily be a problem, but you can return your database to its freshly seeded state at any time by running `rails db:reset`.

Now it's time to talk about [how your `User` model will interact with artists and records](StepThree.md).
