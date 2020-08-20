
### General

| Request | Route | Controller | Result |
| --- | --- | --- | --- |
| GET | /artists/:artist_id | artists#show | Return a single artist *including* that artist's records. |
| POST | /artists/ | artists#create | Create an artist. |
| POST | /artists/:artist_id/records | records#create | Create a new record for the given :artist_id. |
| GET | /artists/search/:search_string | artists#search | Return a list of artists that match the search string. |


### User-specific Info

| Request | Route | Controller | Result |
| --- | --- | --- | --- |
| GET | /users/artists | users#user_artists | Return a list of the artists in the logged-in user's collection. |
| GET | /users/records/ | users#user_records | Return a list of the records in the logged-in user's collection. |
| GET | /users/artists/:artist_id | users#user_records_by_artist | Return a list of the records by a *particular* artist in the logged-in user's collection |
| POST | /users/records/:record_id | users#add_record | Create a new `Purchase` connecting the logged-in user to a `Record`. |
| DELETE | /users/records/:record_id | users#remove_record | Delete the `Purchase` connecting the logged-in user to a `Record`. |


### Auth Routes

| Request | Route | Controller | Result |
| --- | --- | --- | --- |
| POST | /users | users#create | Create new user. |
| POST | /login | users#login | Log in user. |
| GET | /auto-login | users#auto-login | Log in automatically using JWT. |
