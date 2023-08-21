# Putting it All Together: Client-Server Communication

## Learning Goals

- Understand how to communicate between client and server using fetch, and how
  the server will process the request based on the URL, HTTP verb, and request
  body
- Debug common problems that occur as part of the request-response cycle

## Introduction

Just like the last lesson, we've got code for a React frontend and Rails API
backend set up. This time though, it's up to you to use your debugging skills to
find and fix the errors!

To get the backend set up, run:

```console
$ bundle install
$ rails db:migrate db:seed
$ rails s
```

Then, in a new terminal, run the frontend:

```console
$ npm install --prefix client
$ npm start --prefix client
```

Confirm both applications are up and running by visiting
[`localhost:4000`](http://localhost:4000) and viewing the list of toys in your
React application.

## Deliverables

In this application, we have the following features:

- Display a list of all the toys
- Add a new toy when the toy form is submitted
- Update the number of likes for a toy
- Donate a toy to Goodwill (and delete it from our database)

The code is in place for all these features on our frontend, but there are some
problems with our API! We're able to display all the toys, but the other three
features are broken.

Use your debugging tools to find and fix these issues.

There are no tests for this lesson, so you'll need to do your debugging in the
browser and using the Rails server logs and `byebug`.

**Note**: You shouldn't need to modify any of the React code to get the
application working. You should only need to change the code for the Rails API.

As you work on debugging these issues, use the space in this README file to take
notes about your debugging process. Being a strong debugger is all about
developing a process, and it's helpful to document your steps as part of
developing your own process.

## Your Notes Here

- Add a new toy when the toy form is submitted

  - How I debugged:
  1. On seeing this error; "500 (Internal Server Error) in my frontend console, I began my debug process in the server logs.
  2. The headsup in the server logs console, led me to the Toys controller file
  3. Realized that there was a name error. "Toy" instead of "Toys. 

- Update the number of likes for a toy

  - How I debugged:
  1. After looking at the error in my frontend's console, I also took a loot at my server logs console.
  2. The error showed "unpermitted parameter :id"
  3. So, I checked the controller, I added the id to the permit, the error persisted on the frontend but dissapeared on the backend. 
  4. Then I realized that render json was missing. I added that. The frontend console error stopped. 
  5. I deleted the :id which was added to the .permit, and it still worked. 

- Donate a toy to Goodwill (and delete it from our database)

  - How I debugged:
  1. I checked the Network Tab on the frontend, it showed "DELETE 404 (Not Found)"
  2. Afterwards, I checked the Rails Server logs in the backend, it showed "(No route matches [DELETE] "/toys/1")"
  3. So, I went to routes.rb, and added THE the :delete route to handle the DELETE request
