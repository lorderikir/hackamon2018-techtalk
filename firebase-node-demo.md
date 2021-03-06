Theme: Business Class
autoscale: true
text: Roboto, #ffffff
text-strong: Roboto Bold, #ffffff
text-emphasis: Roboto Light Italic
header: Roboto, #ffffff
header-strong: Roboto Strong,#ffffff
header-emphasis: Reklame Script, #ffffff  
code: Fira Code Medium, #FFF, #FFF, #FFF, #FFF, #BBB
background-color: #FFFFFF  
table-separator-color: #DDDEE0
footer: **#Hackamon2018** [MONASH.EDU/STUDENTS/HACKAMON](https://monash.edu/students/hackamon) **|** 14th APRIL 2018 | Copyright Ⓒ Eric Jiang 2018
slidenumbers: false

# Getting Started at Hackathons

## Track 2: Building a MVP with Firebase and ReactJS

![original](assets/firebase-bg.png)

---

# Hi, I'm **Eric Jiang** 👋 <br/><br/>

* Currently, the Project Lead for [monPlan](monplan.apps.monash.edu)
* Co-founded GeckoDM and MARIE.js
* Co-founded and Pitched FutureYou to SMC, now spun that off as a seperate project
* ![](assets/twitter.png) [@lorderikir](https://twitter.com/lorderikir)
* ![](assets/website.png) https://lorderikir.me
* ![](assets/email.png) eric.jiang@monash.edu
* github.com/lorderikir

![original](assets/firebase-bg.png)

---

# Prerequisites

* NodeJS (preferably with YarnPKG)
* An IDE 📝
* An Internet 🌐 Connection

![original](assets/firebase-bg.png)

---

# What is Firebase?

> Firebase is a mobile and web application development platform developed by Firebase, Inc. in 2011, then acquired by Google in 2014.
> -- Wikipedia

We are going to use Firebase Hosting in this demo

![original](assets/firebase-bg.png)

---

# What is ReactJS

ReactJS is a **component-based** that is used to build user-interfaces whether its for websites (Frontend) or hybrid (ElectronJS) applications

![original](assets/firebase-bg.png)

---

![inline](https://i.imgur.com/udYGC3F.png)

![original](assets/firebase-bg.png)

---

# Installing Create-React-App

CRA is a zero-configuration generator tool that can get us started up quickly

```
npm install -g create-react-app

# or if you are using yarn

yarn add -g create-react-app
```

![original](assets/firebase-bg.png)

---

# We will now create our new app.

So after we clone our git repository, we look at using create-react-app into our new directory

```
create-react-app myapp
```

![original](assets/firebase-bg.png)

---

We then go into our new directory and install all the dependencies we need

```
npm install material-ui@next material-ui-icons whatwg-fetch --save

# or

yarn add material-ui@next material-ui-icons whatwg-fetch
```

* We're using fetch polyfill here as `fetch` is built in natively into the browser, and it is not available for IE11 or prior
* We're also using the beta version of material-ui v1 (it will go GA Soon)

![original](assets/firebase-bg.png)

---

# Time for coding! 👨‍💻👩‍💻

## Let's build an app which users can see and search all the rooms within Monash

![original](assets/firebase-bg.png)

---

# Initialise Firebase Project

![inline](assets/fb-console.png)

1.  Go to [console.firebase.google.com/](https://console.firebase.google.com/)
2.  Create a new project
3.  And we're good to go!

![original](assets/firebase-bg.png)

---

# Let's build a Room Card First

```js
// src/components/RoomCard.js

import React from "react";
import { Card, CardMedia } from "material-ui";
import { CardContent } from "material-ui/Card";
import Typography from "material-ui/Typography";

export default function RoomCard({ roomCode, roomLocation, roomPicture }) {
  return (
    <Card>
      <CardMedia
        image={roomPicture}
        style={{
          height: 200
        }}
      />
      <CardContent>
        <Typography variant="subheading">{roomCode}</Typography>
        <Typography variant="title">{roomLocation}</Typography>
      </CardContent>
    </Card>
  );
}
```

![original](assets/firebase-bg.png)

---

We can easily reference this directly in our main component

```js
// src/app.js
import React, { Component } from "react";
import logo from "./logo.svg";
import "./App.css";
import RoomCard from "./components/RoomCard";

class App extends Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h1 className="App-title">Welcome to React</h1>
        </header>
        <RoomCard
          roomCode="S11_LECTURE_HALL"
          roomLocation="17 Rainforest Walk"
          roomPicture="https://www.monash.edu/__data/assets/image/0009/292365/science-lecture-theatre1.jpg"
        />
      </div>
    );
  }
}

export default App;
```

![original](assets/firebase-bg.png)

---

# Now connect it to Firebase

![original](assets/firebase-bg.png)

---

# Firebase Configuration... ⚒️

We will need to setup the configuration for Firebase

```javascript
// src/config/firebase.js

// Import the Firebase modules that you need in your app.
import firebase from "firebase/app";
import "firebase/auth";
import "firebase/database";
import "firebase/datastore";

// Initalize and export Firebase.
const config = {
  apiKey: "MY AWESOME API KEY",
  authDomain: "MY DOMAIN",
  databaseURL: "https://defs-a-secret-project-ddatabae.firebaseio.com",
  projectId: "so-safe",
  storageBucket: "wow-firebase.appspot.com",
  messagingSenderId: "firebase-sender-id-goes-here-i-guess"
};
export default firebase.initializeApp(config);
```

![original](assets/firebase-bg.png)

---

We can also use some API calls!

I recommend you using `fetch` which is a polyfill built into web-browsers, but `axios` is also great for NodeJS Development.

Fetch was installed during the early development as it is not part of IE11 (Legacy Browser support!)

```js
const MONPLAN_API_URI = "monplan-api-au-prod.appspot.com";
fetch(MONPLAN_API_URI + "/api/units")
  .then(resp => resp.json())
  .catch(err => console.error(error))
  .then(data => console.log(data));
```

![original](assets/firebase-bg.png)

---

# Any questions? 🤔

![original](assets/firebase-bg.png)
