# advanced node starter 1

## project walkthrough

* clone advanced node starter. - [here](https://github.com/StephenGrider/AdvancedNodeStarter)
* projects include CRA client and backend nodejs server.

### nodejs project structure

* body parser, cookie session, passport - express middleware.
* auth routes, blog routes.
* blog routes has requireLogin middlewares for the user login.

#### database

* mongoose ORM.
* blog, user model.

-----

* Will add dependencies - should install client dependencies.

* install two sets of dependencies.

## key customization

* run `npm run dev` to run both client and server.
* we use google oauth for authentication.

----

* should make personal copy of mongodb.
* use mlab.

## mongodb creation

* connect mlab mongodb.

## routes walkthrough

* add first advanced feature.
* there's blog creation feature, login feature.

### routes

* `/auth/google`
* `/auth/google/callback`
* `/auth/logout`
* `/api/current_user` - get the current user

----

* `/api/blogs/:id`
* `GET /api/blogs` - get all blogs that belongs to the user.
* `POST /api/blogs`

# section 4 - data caching in redis

## mongodb query performance

* every time user refreshes the page, you sends two request - `/api/current_user`, `api/blogs`.

* This might not be that big, but if the server scales, it becomes an issue.

-----

* for mongodb, it is an issue.

* if you sends query to mongodb, it indexes some record.

* one collection for blogs, one collections for users.

* query is sent to index - an efficient data structure.

* index checks records to see if it matches the query.

* if index is targeted for certain property, it should check every single collection - like id property.

* id is fine, but how about title? or contents? index for these keys does not exist, causing some race condition.

* default behavior - check every documents, full collection scan. extremely expensive.

----

### two ways to solve

* 1 - make an index for that properties.
* but, if you add more indices, it takes more disk space, and more difficult to add documents to that.
* and can't figure out what indices to construct for title, content, etc.

* 2 - cache the request and response.

## query caching layer

* will create cache server.

### what is caching layer

* react <-> express <-> mongoose <-> cache server <-> mongoDB

* cache server - check to see if the exact query ever existed before.

* if not, store result of query on cache server.

* if cache server sees request, it doesn't send request to mongodb, but immediately send back to mongoose.

-------

* cache server - key value pair data structure.

* key - might be id, value - the result.

* just the key value pair lookup.

-----

* how the data in cache server is going to be expired?

* writing is going to mongodb always.



























































