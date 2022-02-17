# Firebase gmail auth

This library is supposed to be a tiny helper to wrap firebase and being able to login with gmail in any tiny little html app to be able to use the JWT for API calls.

Before anything else your project needs to import the following three files, two of which are firebase and one, this library:
```html
<script src="https://www.gstatic.com/firebasejs/8.3.2/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/8.3.2/firebase-auth.js"></script>
<script src="..."></script>
```

## Usage

When you spin up your page, at the end of the body or if you are using React/VueJS when the component starts, call the `initFirebaseAuth` function that takes three required configuration parameters and callbacks for login and logout and you are all set.

I recommend controlling all rendering in your UI based on these two events as either one of them are guaranteed to be called on startup, either as you are "logged out" if you haven't logged in yet or your session will resume from before.

I use module imports for this:

```html
<script type="module">
import { initFirebaseAuth, googleLogin, logout } from './firebase-auth.js';

initFirebaseAuth({
  apiKey: 'xxx',
  authDomain: "xxx.firebaseapp.com",
  projectId: 'xxx',
  loggedIn: (user, token) => {
    $('#loggedIn').show();
    $('#loggedOut').hide();
  },
  loggedOut: () => {
    $('#loggedIn').hide();
    $('#loggedOut').show();
  }
});
</script>
```

To then login or logout you use the two helper functions `googleLogin(onError)` and `logout`. If you wired up your UI to be rendered with the callbacks above, your UI will automatically update once either of these functions complete.

In the off-chance that login fails, the `googleLogin` takes a callback to handle the error.