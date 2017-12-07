# Extra topics

This is a list of topics you should be familiar with that may or may not have been covered in the Rails book.

## How to use this doc

* Fork this document on Github
* Answer/complete the sections below and commit your changes to your forked version of this doc.
* Start by editing the space below to include your name and date (note: you may need to review [Markdown syntax](https://daringfireball.net/projects/markdown/syntax) first)

```
jonathan mosesman 11-29-17
```

* Next, create a new branch called `name-and-date`, commit your change, push it to Github, and create a pull request (PR).
* Review the pull request and merge it.
* Continue with that process for the remaining sections (you don't have to do a PR every time, you can merge from the command line if you want).


The sections below can be done in any order, so feel free to skip around if you get stuck.


## Build a personal blog

Every developer needs a personal blog/site. Blogs are a great resource for other developers, and you'd be surprised what you know that someone else is trying to figure out—no matter how simple it seems. The best way I've heard it put is, "Write to yourself from 6 months ago about what you wish you knew then."

Blogs are also social proof that you know some things. Most of the time, blogs are built using what are called "static site generators." The idea is that for a blog that justs loads static HTML pages, you don't need a full-fledge app with a database, routing, controllers, etc. Just a static website is good enough. So:

* Build a static site using [Jekyll](https://jekyllrb.com/) with a "hello world" post (add real posts too if you want to).
* Deploy it to GitHub pages. 
* (BONUS) Setup a custom root and sub domain to point to that site (i.e., "johnmosesman.com" and "www.johnmosesman.com").
* Put the link to your site below

```
https://jlmosesman.github.io/My-Blog/
```

## APIs

### What is an API?

```
Application Program Interface. API's are ways to give universal access to information or assets you want to share. Developers can "plug in" their apps and data to deliver to users.
```

### What status codes are _usually_ returned for the following responses, and what do they mean?

- Success: ` 2xx: action was successfully received, understood, and accepted `
- Created: ` 201: typically the reponse of a PUT request, the request succeeded and a new resource has been created `
- Unauthorized: ` 401: the request requires user authentication `
- Unprocessable entity: ` 422: the request was well-formed but was unable to be followed due to semantic errors `
- Not Found: ` 404: the server cannot find the requested resource; a URL isn't recognized or a resource doesn't exist `
- Internal Server Error: ` 500: the server has encountered an unexpected error `

### What are the most common HTTP verbs sent with a HTTP request, and what CRUD actions do they map to?

```
POST: create
GET: read
PUT: update/replace 
PATCH: update/modify
DELETE: delete
```

### Build a Rails API that returns JSON for standard CRUD actions on a "user" object.

This is probably the largest task in this list, but APIs are everywhere. Take your time and go step-by-step.

- (Maybe) look up what JSON is
- Create a rails app using the `--api` flag
- Put it under the `/api` namespace
- Write tests for every endpoint
- Use [cURL](https://curl.haxx.se/) to hit each API endpoint (show the request you made and the responses for each)

```
jonathans-imac:todos-api jonathanmosesman$ http :3000/todos
HTTP/1.1 200 OK
Cache-Control: max-age=0, private, must-revalidate
Content-Type: application/json; charset=utf-8
ETag: W/"4f53cda18c2baa0c0354bb5f9a3ecbe5"
Transfer-Encoding: chunked
X-Request-Id: a680a977-4377-4bfe-a50f-9066db2bd3aa
X-Runtime: 0.124416

[]

jonathans-imac:todos-api jonathanmosesman$ http POST :3000/todos title=Mozart created_by=1
HTTP/1.1 201 Created
Cache-Control: max-age=0, private, must-revalidate
Content-Type: application/json; charset=utf-8
ETag: W/"70f92e34030a9fdd1c5997027dce917a"
Transfer-Encoding: chunked
X-Request-Id: e4cfc848-58f4-4982-8174-2c534f024353
X-Runtime: 0.008559

{
    "created_at": "2017-12-05T00:03:38.605Z",
    "created_by": "1",
    "id": 1,
    "title": "Mozart",
    "updated_at": "2017-12-05T00:03:38.605Z"
}


jonathans-imac:todos-api jonathanmosesman$ http :3000/todos
HTTP/1.1 200 OK
Cache-Control: max-age=0, private, must-revalidate
Content-Type: application/json; charset=utf-8
ETag: W/"3b2a4e6378a29a688f8bb06c67a42e13"
Transfer-Encoding: chunked
X-Request-Id: 11146295-23a0-4329-918e-d4a1a0627407
X-Runtime: 0.002143

[
    {
        "created_at": "2017-12-05T00:03:38.605Z",
        "created_by": "1",
        "id": 1,
        "title": "Mozart",
        "updated_at": "2017-12-05T00:03:38.605Z"
    }
]

jonathans-imac:todos-api jonathanmosesman$ http PUT :3000/todos/1 title=Beethoven
HTTP/1.1 204 No Content
Cache-Control: no-cache
X-Request-Id: de5603d9-f6d1-41b1-b9ae-9909d974ec9f
X-Runtime: 0.005578

jonathans-imac:todos-api jonathanmosesman$ http :3000/todos
HTTP/1.1 200 OK
Cache-Control: max-age=0, private, must-revalidate
Content-Type: application/json; charset=utf-8
ETag: W/"30a4fc8f763c1979b638997a1ea7a1cb"
Transfer-Encoding: chunked
X-Request-Id: 465a75fb-e75a-465b-b6a5-ee8834ca7e88
X-Runtime: 0.001703

[
    {
        "created_at": "2017-12-05T00:03:38.605Z",
        "created_by": "1",
        "id": 1,
        "title": "Beethoven",
        "updated_at": "2017-12-05T00:05:02.421Z"
    }
]


jonathans-imac:todos-api jonathanmosesman$ http DELETE :3000/todos/1
HTTP/1.1 204 No Content
Cache-Control: no-cache
X-Request-Id: 3589d73d-47ea-458b-ac31-21f91795ea3b
X-Runtime: 0.012756

jonathans-imac:todos-api jonathanmosesman$ http :3000/todos
HTTP/1.1 200 OK
Cache-Control: max-age=0, private, must-revalidate
Content-Type: application/json; charset=utf-8
ETag: W/"4f53cda18c2baa0c0354bb5f9a3ecbe5"
Transfer-Encoding: chunked
X-Request-Id: 05e160d9-eff5-4455-a38e-86cd93ebc1d2
X-Runtime: 0.001479

[]
```

After you've completed the above, put the "update" and "delete" endpoints behind token authentication. To do this:

* Assign each user a secure, randomly-generated token
* In the HTTP request, pass the token via the "Authorization" header.
* Parse the HTTP header and try to look up the user that matches the token. Based on the result, either return unauthorized (see status codes above) or allow the action to go through.

```
jonathans-imac:todos-api jonathanmosesman$ http :3000/todos
HTTP/1.1 422 Unprocessable Entity
Cache-Control: no-cache
Content-Type: application/json; charset=utf-8
Transfer-Encoding: chunked
X-Request-Id: 3483eff4-8675-4652-8a4a-82ea7e338f66
X-Runtime: 0.105706

{
    "message": "Missing token"
}


jonathans-imac:todos-api jonathanmosesman$ http :3000/signup name=ash email=ash@email.com password=foobar password_confirmation=foobar
HTTP/1.1 201 Created
Cache-Control: max-age=0, private, must-revalidate
Content-Type: application/json; charset=utf-8
ETag: W/"1de3c98ca31e54690844618584fcaa32"
Transfer-Encoding: chunked
X-Request-Id: b17b9fb2-da62-4b95-bd80-42d777f215b8
X-Runtime: 0.162254

{
    "auth_token": "eyJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxLCJleHAiOjE1MTI1MjYxMzd9.EeV-r4zhsUgVOUdWIht55vLcKwgMZuB0u969KzcVknE",
    "message": "Account created successfully"
}


jonathans-imac:todos-api jonathanmosesman$ http :3000/todos Authorization:'eyJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxLCJleHAiOjE1MTI1MjYxMzd9.EeV-r4zhsUgVOUdWIht55vLcKwgMZuB0u969KzcVknE'
HTTP/1.1 200 OK
Cache-Control: max-age=0, private, must-revalidate
Content-Type: application/json; charset=utf-8
ETag: W/"4f53cda18c2baa0c0354bb5f9a3ecbe5"
Transfer-Encoding: chunked
X-Request-Id: 71dff1ef-61b8-4f26-a38a-0f3ee483df64
X-Runtime: 0.011623

[]


jonathans-imac:todos-api jonathanmosesman$ http POST :3000/todos title=Beethoven Authorization:'eyJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxLCJleHAiOjE1MTI1MjYxMzd9.EeV-r4zhsUgVOUdWIht55vLcKwgMZuB0u969KzcVknE'
HTTP/1.1 201 Created
Cache-Control: max-age=0, private, must-revalidate
Content-Type: application/json; charset=utf-8
ETag: W/"5cadad7331fc70688395abeff22c3480"
Transfer-Encoding: chunked
X-Request-Id: 503cdd7f-321c-40a0-a673-4a7b79d041d9
X-Runtime: 0.007857

{
    "created_at": "2017-12-05T02:11:34.309Z",
    "created_by": "1",
    "id": 2,
    "title": "Beethoven",
    "updated_at": "2017-12-05T02:11:34.309Z"
}


jonathans-imac:todos-api jonathanmosesman$ http :3000/todos Authorization:'eyJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxLCJleHAiOjE1MTI1MjYxMzd9.EeV-r4zhsUgVOUdWIht55vLcKwgMZuB0u969KzcVknE'
HTTP/1.1 200 OK
Cache-Control: max-age=0, private, must-revalidate
Content-Type: application/json; charset=utf-8
ETag: W/"35e72204f3dd5178d1bd61729eb06acb"
Transfer-Encoding: chunked
X-Request-Id: b72b8607-9719-407e-9085-bdb80cf94e6b
X-Runtime: 0.002217

[
    {
        "created_at": "2017-12-05T02:11:34.309Z",
        "created_by": "1",
        "id": 2,
        "title": "Beethoven",
        "updated_at": "2017-12-05T02:11:34.309Z"
    }
]
```

## CSS frameworks (Bootstrap/Foundation)

Most companies use a CSS framework to give them easy page layouts and mobile responsive sites. You should be familiar with the concepts of the two leading frameworks: [Bootstrap](http://getbootstrap.com/) and [Foundation](https://foundation.zurb.com/).

1. Create a simple HTML page (doesn't have to be a Rails app) with two rows and a 4-3-2-up grid for large-medium-small screens respectively
2. Do this by including the Bootstrap framework files directly into the `<head>` or `<footer>` elements.
3. Add a README.md file with a description and a screenshot of the page
4. Push it up to Github and put the link below.

Next, do the same thing but use the ruby gem for Bootstrap instead of including it directly.

Finally, do the same thing as above but using Foundation. Put the Github links below.

```
link-to-bootstrap-page
link-to-bootstrap-rails-app
link-to-foundation-page: https://jlmosesman.github.io/foundation-project/ (https://github.com/jlmosesman/foundation-project)
link-to-foundation-rails-app
```

## jQuery

"Modern JS" has evolved past jQuery and will scoff at this, but jQuery is still used in a lot of places, and the concept of events and triggers is something you should at least be familiar with.

1. Include jQuery in an HTML page (doesn't have to be a Rails app)
2. Using vanilla HTML/CSS, create a simple page that has two paragraphs—one visible and one hidden.
3. Add a button with text "Toggle" to the page, and using jQuery, when the button is pressed toggle the visible paragraph to be hidden, and the hidden to be visible.
4. Next, add another button with text "Hover" that toggles the paragraphs only while your cursor is hovering over the button.

## Command line stuff

### vim 

I have this section only as a way to get familiar with basic vim commands, as they are often used in conjunction with editing git commits. At some point you will want to consider switching to a more powerful text editor than sublime/atom/etc., but those are perfectly fine for now.

1. At the command line, type `vimtutor` and follow its instructions. This should take ~30min.

## git / bash

### Tutorial

Git can do a lot of things, and it's not always super obvious. I would recommend reading through [this tutorial](https://www.atlassian.com/git/tutorials/setting-up-a-repository) with the aim of trying to learn what you can, and not worrying about 100% mastery yet.

### Some practice

Using the command line only:

1. Create a new folder somewhere on your machine
2. Change into the folder and initialize git
3. (Try to use the command line for this) Create a text file and open it in your editor (or vim!!)
4. Write something in there and commit the change with a message.
5. Create a repo on Github and push up the file.

Next:

6. Write something else and commit again locally with another message.
7. Amend your previous commit message and put `(AMENDED)` at the end of the message.
8. Run `git reset --hard origin/master`. Oh no your last change is gone!
9. Use `git reflog` to recover your change.

Save your commands and paste them below.

```
$ your commands here
```

## dotfiles

Dotfiles are configuration files for programs you use on the command line. By convention most of them end in "rc" (`.bashrc`, `.vimrc`, `.railsrc`) and the file name starts with a dot (which means "hidden" file).

Dotfiles are very powerful and do a lot of things, but for now let's use two simple use cases.

### aliases

You're going to type certain commands _over and over and over and over_. Things like `rails db:migrate`, `git status`, and `bundle install`. Eventually you will get tired of typing these things, and you will want a faster way—enter aliases.

If you're on Mac OSX, you're probably using `bash` as your default command line shell. Bash has a configuration file named `.bashrc`. This file might already exist in your home directory on your machine. Run the following to check: 

```
$ ls -a ~/ | grep bashrc
```

That command lists all files in your home directory (`~/`) and passes the output (via the pipe operator `|`) to the `grep` command, which searches for the text `bashrc`. The `-a` flag means include "hidden" files—or these whose file names start with a dot (like our `.bashrc` does).

If you see the `.bashrc` file as a result that's great. If not, make the file like this:

```
$ cd    # `cd` with no arguments is a shortcut to the home directory
$ touch .bashrc
```

Run the search command again. You should see the new file there now.

Open up `.bashrc` and add the following lines:

```
alias bi="bundle install"
alias gs="git status"
```

Save the file, and run the `source` command to reload the configuration file in your shell: `$ source ~/.bashrc`.

Now switch to a directory that has a git repo initialized and type `gs`. You should see the result of `git status` printed out.

I've made aliases for _tons_ of commands. There are some commands that I can't seem to type correctly, so I just alias my most common misspellings to the actual command. For example: `alias rbnev="rbenv"`

### Configuration

Dotfiles aren't just for aliases, they're intended for configuration. Create a new file in your home directory called `.railsrc`, and put the following:

```
-B # Skip bundle
-d postgresql
```

Source the file, and the next time you create a new rails project it will skip bundling at the start, and default your database to Postgres instead of sqlite.


## SQL

TODO
