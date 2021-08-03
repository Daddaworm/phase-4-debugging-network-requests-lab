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

```sh
bundle install
rails db:migrate db:seed
rails s
```

Then, in a new terminal, run the frontend:

```sh
npm install --prefix client
npm start --prefix client
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
    -first read the errors on brower network tab.  Pointed to uninitialized constant Toys in toy controller. error 500.
    -went to controller.  Since it was a post, found the create action and reviewed.  Did not see anything wrong initially.
    -we to routes to ensure it was set up correctly since thats the first thing the request comes through.  Did not find anything wrong with routes.
    -read error a second time and noticed that if it was a create method called on the class, it should not be plural.   
    -went to controller and looked at the create method.  Noticed it was plural.  Changed it to singular.
    -went back to front end and submitted another toy.  Checked network tab and saw object returned from backend.  Validated it appeared on front end...and it did. Problem solved.

- Update the number of likes for a toy

  - How I debugged:
    -first tested button by pressing and seeing if it updated in brower.  It did not.
    -went to network tab to see what was being returned in preview.  It was blank
    -checked routes to ensure it was correct and it was.
    -checked controller action and it appeared good at first inspection.
    -went back to front end and opened console.  Tested button and saw error "unexpected end of JSON input and immediately knew what error was (json was not being returned)
    -went back to controller action and saw there was no render for the json data.  
    -added render json: toy
    -went to front end and tested again...Like then updated on browser.  Check network to ensure json returned from backend with updated like count.  It was!!  Problem solved.

- Donate a toy to Goodwill (and delete it from our database)

  - How I debugged:
    -tested button with console open.  Noticed error 404 not found when button pressed.
    -checked network tab and saw error stating no route matches DELETE.
    -went to routes.rb and immediately noticed resources did not have a DELETE in its route.
    -added the Delete to routes
    -tested buttong again.  Got error undefined (not found 404)
    -realized route should be named destroy and not delete.  Updated to correct name and tested buttong again.
    -problem solved.  toy deleted.

