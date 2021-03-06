##README.md

#Meetup - Angular 2 Firebase 02

Based on 'Deploy Angular 2 CLI Apps to Firebase' at https://coryrylan.com/blog/deploy-angular-2-cli-apps-to-firebase

In this post we're going to cover how to get an Angular 2 application up and running and deploy it to Firebase. First lets cover how to use the Angular CLI to help bootstrap our application�s build process.

##Angular 2 CLI

The Angular 2 CLI is an officially supported project by the Angular team. You can find more information at [https://cli.angular.io](https://cli.angular.io/). First we will install the Angular CLI tool. To install we install via NPM running the following command: ```npm install angular-cli -g```. This will install the CLI globally to our machine to help us create new Angular projects.

Note: [Angular CLI Reference](https://cli.angular.io/reference.pdf)

Once installed we can create a new Angular 2 app by running the following command: ```ng new my-cool-app```. Next open your app in your favorite editor (here: Visual Studio Code).

You should see something similar to this (as of CLI beta 10):

```javascript
my-cool-app
  > e2e
  > node_modules
  > src
  .editorconfig
  .gitignore
  angular-cli.json
  package.json
  protractor.conf.js
  README.md
  tslint.json
```

### Run the Development server
From inside the my-cool-app folder, run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

You should see in your browser:

***app works!***

Inside my-cool-app/src/app/app.component.ts change the following line of code from:

```javascript
  title = 'app works!';
```

to:

```javascript
  title = 'my cool app works!';
```

When saving the file, witness in the terminal window that the source code is automatically re-processed and the text in the browser now reads:

***my cool app works!***

### Running unit tests

From inside the my-cool-app folder, run ```ng test``` to execute the unit tests via [Karma](https://karma-runner.github.io). The test should fail if the title on the page is ***not*** 'app works!'

###Build for Production

I won't cover all the CLI commands in this post. I recommend checking out the [CLI Docs](https://cli.angular.io/). We will just start with running ```ng build --prod```. This command runs a build for our project but with additional production optimizations such as bundling and minification. Now your project should have a dist/ directory. This is where all of our compiled ready to deploy code is located every time we run a build.

##Firebase CLI

So now that we have learned how to use the Angular 2 CLI to package up our app for deployment we will use the Firebase CLI to create a live hosting project to deploy to.

First you will want to log into Firebase and go to [https://console.firebase.google.com/](https://console.firebase.google.com/). Once in the console select �Create New Project�. For our project we will name it �my-cool-app�.

- screenshot goes here - 

Now that we have a project created lets go back to the command line. Next we install the Firebase CLI via NPM. In your console run the following command: ```npm install -g firebase-tools```. Once installed run ```firebase login --interactive``` to login to your Firebase account.

##Deployment Setup

Now that Firebase CLI is installed, at the root of your Angular CLI project run ```firebase init```. This will walk through the steps of setting up your app to be deployable to Firebase Hosting.

- screenshot goes here - 

Select the Hosting option in the command line. Next select our project ```my-cool-app``` that we created earlier. Next it will ask what file to use for the Firebase real time database rules. For now you can just use the default.

***The next step is important!*** The cli will ask what folder to use as the public directory. For our project we want to use the ```dist/``` directory instead of Firebase�s default ```public/``` directory. So type in the command line ```dist```.

Next it will ask if this is a single page app and if it should rewrite all urls to ```index.html```. For our app select ***yes***. If it asks to over write the ```index.html``` file select ***no***. Now your app is ready for deployment! In the root of your app you should have a new file ```firebase.json``` file that helps the Firebase CLI know how to deploy our application. Now run ```firebase deploy```. Firebase will provide domain that you can configure to a custom domain in the console. Now if we open our browser we will see something similar to the following:

- screenshot goes here -

Now that we have created an Angular 2 project and deployed it to Firebase I recommend digging into more of the [Angular 2 CLI](https://cli.angular.io/) and the [Firebase Features](https://firebase.google.com/features/). A few things to note, the CLI at the time of this writing is in Beta 10. A large change is in the works for Beta 11 to switch the underlying build system to [Webpack](https://webpack.github.io/). This post will be updated with those changes. Also in future versions of the Angular CLI will possibly have Firebase integration and deployment built in. Also as of Beta 10 of the Angular CLI production build do not have a versioning system to bust browser cache. This should be addressed in upcoming versions.
