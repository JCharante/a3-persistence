## Triage V2

Try it out at https://a3-jcharante.glitch.me


Web App Source Code: https://github.com/JCharante/triage-spa-v2

API Server Source Code: https://github.com/JCharante/triage-server-v2

Despite there being two repositories, the webapp and API server are on the same glitch project.

Triage helps you keep track of tasks you have to do. It has support for recommended deadlines, and hard deadlines, as for many classes they have recommend doing certain problems after lecture but may only collect homework once a week. There's support for multiple levels of importance and for difficulty. It uses all of the just mentioned filed to calculate a priority score, which is displayed on the web app and is used to sort the list of tasks. This differentiates itself from other existing options.

Sound familiar? This is because it's a rewrite from last week.

![image](https://user-images.githubusercontent.com/13973198/65221797-bac08800-da8b-11e9-86f0-606fff259c5b.png)


Originally I attempted to have this work out of two glitch.me's. Unfortunate I couldn't fix the cors issues that would randomly happen, so I used express.static to serve the files. Originally I avoided it because it seems like a pain, but both solutions required unzipping a zip file, and thankfully express.static works very well.

I used Quasar Framework. It's more than just a CSS Framework. It has implemented Material Design components, but it also comes with pre-configured webpack and stylus among other things.

For authentication, users can log in or create an account to receive a sessionKey, which are saved in MongoDB. We wanted to use a document store storage solution because of the flexibility with being able to support new fields on the client without making any additional changes to the server.

Usage of middleware:

- cors
  - This is used during development, especially when we don't need to run the local api server but want to make API calls from our locally client.
- body-parser
  - This is used to help parse urlencoded data that we receive
- express
  - We use the json parser and the static middlewares to serve the website
- morgan
  - We use this to log requests to our server
- passport
  - We use this to handle user credentials
  
Meeting requirements:
  - HTML Input Tags and Forms
    - We have a Floating Action Button (FAB) on the lower right corner to add new items
    - We use dropdown lists for selecting difficulty, importance, and status
    - We have buttons to log in or confirm prompts
    - We have input boxes to enter credentials or data
    - We have date choosers
  - There is code on the server to write, modify, and delete tasks.

## Technical Achievements
- **MongoDB**: I used the Node.js driver for MongoDB, enabling me to quickly write the backend code with its easy queries and have the peace of mind with its data duplications, rather than storing it on the FS on glitch.
- **Soft Deletes**: Since it's trendy to not actually delete a user's data, when you click to delete a task, we perform a soft delete where the data is no longer returned by the API, but is still available for data harvesting.
- **Local Storage**: To improve UX, I am storing the sessionKey to the local storage and clearing it on log out so that when you refresh the page you don't have to log in again, as I am using sessionKeys generated on login/signup rather than cookies.
