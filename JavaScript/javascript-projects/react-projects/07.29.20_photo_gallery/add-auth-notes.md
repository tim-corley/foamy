## Add Authentication

https://firebase.google.com/docs/auth/web/start
https://blog.logrocket.com/user-authentication-firebase-react-apps/

add react-router

1. add firebase auth to the project

```javascript
// config.js
import "firebase/auth";
//...
const projectAuth = firebase.auth();
// ...
export { projectStorage, projectFirestore, projectAuth, timestamp };
```

2. enable email/password & google login method via the firebase project authentication console

3. add [React Router](https://www.npmjs.com/package/react-router) to the project

4. create components
   - Signing in & signing out
   - Signing up with Google or email/password
   - Password reset
   - Profile Page
   - Landing Page
