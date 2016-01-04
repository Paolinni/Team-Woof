# City Quest #
  > **Looking for a new adventure while on vacation or even in your hometown?**  
  > Use the City Quest app to search for "quests" that align with your interests.  
  > Once you've chosen a quest, follow the quest's steps and have fun!  
  > **Have an awesome agenda for a day in the city that you would like to recommend to others?**  
  > Get creative and turn that agenda into a "quest" with the City Quest app.

## How to Get Started ##
  > Search your destination and complete a quest of your choosing.

## Customer Quote ##
  > "This made my trip to Miami super easy. Thanks son!" -Mom

# Technical Documentation

## Getting Started

```
$ git clone https://github.com/teamwoof/Team-Woof.git
$ cd Team-Woof
$ bower install
$ npm install
$ node server/server.js
```

Now visit [localhost:3000](http://localhost:3000/)

### Architecture Overview

The tech stack is MongoDB, Express, Angular, and Node.

The app starts with client/city/city.html as the root '/' view.
The controller in client/city/city.js will take in the user's desired city
and save it away in the service in client/services/questStorageService.js.
Next, the controller in city.js will redirect to the client/questList/questList.html.

The controller in client/questList/questList.js will, upon loading, call into
client/services/questStorageService.js to fetch all quests that are
associated with the selected city that was saved to questStorageService.js
by the previous page/controller.  By clicking on a quest title in
questList.html, the app will route to client/questView/questView.html while passing
the corresponding quest._id as a routing parameter to client/questView/questView.js.

The controller in questView.js will receive the quest ID as a routing
parameter and then use the service in questStorageService.js to fetch
that quest's information and then place a marker for each quest step location
on a Google Map embedded in questView.html.

Another aspect of questView.html to call out is the usage of a custom directive,
client/questView/stepViewDirective.js.  This directive will use
the stepViewTemplate.html to ng-repeat all the individual steps in a quest.
The motivating reason for creating a custom directive was to dynamically
populate the Google Street View for each step of the quest.
To accomplish this, we pass a function to the directive's "link" property.
This "link" function will get passed the current $scope and the
directive's html element (which we have to drill down into to ultimately
get to the Street View Div).  Using the scope passed in. we have access
to the "step" from the ng-repeat ('step in quest.steps').  Then, with
each quest step, we take its latitude and longitude and create
a Google Street View.

