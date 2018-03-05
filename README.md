# OnSignal

![NPM Version](https://img.shields.io/npm/v/onsignal.svg) <img src="https://travis-ci.org/jonhue/onsignal.svg?branch=master" />

A OneSignal API wrapper simplifying user targeted cross platform notifications. OnSignal consists of a JavaScript and a Rails API:

* [JavaScript API](#usage): Handle user subscriptions to OneSignal in your frontend code.
* [Rails API](https://github.com/jonhue/onsignal-rails): Attach OneSignal players to user records provided by an authentication solution.

---

## Table of Contents

* [Usage](#usage)
    * [Overview](#overview)
    * [Subscribing](#subscribing)
    * [Unsubscribing](#unsubscribing)
    * [Additional functions](#additional-functions)
* [To Do](#to-do)
* [Contributing](#contributing)
    * [Contributors](#contributors)
    * [Semantic versioning](#semantic-versioning)
* [License](#license)

---

## Usage

Handle user subscriptions to OneSignal in your frontend code.

### Overview

```javascript
import 'onsignal/dist/OneSignalSDK';
import OnSignal from 'onsignal';

document.addEventListener( 'ready', () => {
    const onSignal = new OnSignal( 'OneSignal App ID', {
        autoRegister: false
    });

    // Object to call OneSignal API from
    onSignal.oneSignal;

    // Current users player ID
    onSignal.playerId;

    // Current users permission
    onSignal.permission;
};
```

#### Options

Pass options to OneSignal's `push(['init', {...}])` function as a hash. Default values are:

* `autoRegister` Automatically try to subscribe the user when loading a page. Accepts a boolean. Defaults to `false`.
* `persistNotification` If set to `false `, automatically dismisses notifications after ~20 seconds in Chrome Desktop v47+. Accepts a boolean. Defaults to `false`.
* `welcomeNotification` Hash configuring the default OneSignal welcome notification. Accepts a hash. Defaults to `{ disable: true }`.
* `notifyButton` Hash configuring the default OneSignal notify button at the bottom right of the screen. Accepts a hash. Defaults to `{ enable: false }`.

### Subscribing

Just call `onSignal.subscribe();` and OneSignal will ask your user for permission to send notifications if he is not subscribed yet. _On the following request an existing `Device` object will either get updated or a new one will get created. (if using the Rails API)_

#### Options

Pass options to OneSignal's `registerForPushNotifications()` function as a hash. Default values are:

* `modalPrompt` Whether or not to use a custom prompt instead of the browsers default to ask for permission. Accepts a boolean. Defaults to `false`.

### Unsubscribing

**Note:** You most likely don't want to let your users unsubscribe from receiving notifications, but instead allow them to manually disable receiving any new notifications. For that purpose use the [notifications-rails](https://github.com/jonhue/notifications-rails) gem, which adds a notification API and detailed user settings.

If you want to completely remove a user from OneSignal, call `onSignal.unsubscribe();`.

### Additional functions

```javascript
// Check if a user is subscribed to OneSignal
onSignal.isSubscribed()
```

---

## To Do

[Here](https://github.com/jonhue/onsignal/projects/1) is the full list of current projects.

To propose your ideas, initiate the discussion by adding a [new issue](https://github.com/jonhue/onsignal/issues/new).

---

## Contributing

We hope that you will consider contributing to OnSignal. Please read this short overview for some information about how to get started:

[Learn more about contributing to this repository](CONTRIBUTING.md), [Code of Conduct](CODE_OF_CONDUCT.md)

### Contributors

Give the people some :heart: who are working on this project. See them all at:

https://github.com/jonhue/onsignal/graphs/contributors

### Semantic Versioning

OnSignal follows Semantic Versioning 2.0 as defined at http://semver.org.

## License

MIT License

Copyright (c) 2018 Jonas Hübotter

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
