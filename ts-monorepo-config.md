# How to configure your TS mono repo with shared dependencies, interfacas, and utils with Expo, NextJS, Node, and Firebase on Macos

Have you ever been in that situation where you're the principal developer on a project, and the amount of repositories you manage have so many dependencies, interfaces and utils that they share that it's now becoming a hassle to just have the different codebases just work together?

If yes, that's me too, and I'm solving it, and giving you a simple step-by-step process to just have everything just work.

To do this, let's get our environment and multiple projects setup. I'll be using Typescript with:

- React Native Expo for our mobile-web crossplatform frontend
- NodeJS, deployed as microservices on the backend
- NextJS frontend for the admin panel, where you can view the fancy analytics

Let's create the starter code and have the setup done for these projects:

1. Expo app Startup

To create the expo app, go to the root directory 'monorepo-ts-config' and run:

```
npx create-expo-app@latest frontend
brew update && brew install watchman
```

This will create the expo application, and install watchman. (The given code is for macOS)

Now, run ``npx expo start` in the frontend directory(don't forget to press "w" for web and "i" for ios!) to see your sweet react app. Voila!

NOTE: If you're on macOS, and you see "Xcode must be fully installed before you can continue", even though you've already install XCode, you might need to run `sudo xcode-select -s /Applications/Xcode.app/Contents/Developer` .

2. NextJS app setup

In the root directory, run `npx create-next-app@latest`, and say yes to all the defaults. I'm naming my app admin for the admin console, and I'm configuring it to use Typescript, with Tailwind CSS and ESLint.

To startup the app, run `npm run dev` and visit localhost:3000.

3. Firebase NodeJS serverless app setup

Go to your firebase console, and create a project. I'll call mine the same as my repo: 'monorepo-ts-config'

Create your backend folder at root, and download the necessary packages.

```
mkdir backend && cd backend
npm install firebase-functions@latest firebase-admin@latest --save
npm install -g firebase-tools
```

Now, login from the cli using `firebase login`. Complete necessary steps to login as specified.

Initialize the project using `firebase init`, and select your preferred services. I will be using firestore, storage and cloud functions. I could also choose to host my frontend using hosting, but not right now.

If you're using any firebase services(firestore, storage, functions, etc), make sure you've created or enabled the same on the firebase console first, i.e. create your database, storage bucket, and ensure to link your billing account if using functions.

4. Create Shared Directory
   Create a shared directory which the above 3 projects will use to share interfaces, utility functions. The shared dependencies will be managed by the root directory

## We can finally get started!
