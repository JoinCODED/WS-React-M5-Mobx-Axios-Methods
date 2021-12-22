We have our data ready in the backend. But how can we send a request to the backend to fetch them? We will use a JavaScript library called `axios`.

1. Let's start with installing it

```shell
  $ npm install axios
```

2. Let's import `axios` in our store

```javascript
import axios from "axios";
```

3. In `fetchCookies`, we will call `axios`. We need to tell `axios` the request's method. In this case our method is `get` since we're `get`ting data.

```javascript
fetchCookies = () => {
  axios.get();
};
```

4. `get` method requires one argument, which is the URL of the request. Our backend is running on `localhost:8000`, and our cookies are on the path `/cookies`. So this will be our path:

```javascript
fetchCookies = () => {
  axios.get("http://localhost:8000/cookies");
};
```

5. `axios.get` will return the cookies list, so we need to save them! Let's console log them:

```javascript
fetchCookies = () => {
  const response = axios.get("http://localhost:8000/cookies");
  console.log("fetchCookies -> response", response);
};
```

6. Let's try it out. We got a Promise.. But we can't access the data this way. Since `axios` is asynchronous, we need something that will tell it to wait. We will use the statement `await` and place it right before `axios`, which means wait for axios to finish before saving its value inside `response`.

```javascript
fetchCookies = () => {
  const response = await axios.get("http://localhost:8000/cookies");
  console.log("fetchCookies -> response", response);
};
```

7. We got an error! `Can not use keyword 'await' outside an async function`

8. We can't use `await` without her soulmate, `async`. `async` basically turns our function to an asynchronous function

```javascript
fetchCookies = async () => {
  const response = await axios.get("http://localhost:8000/cookies");
  console.log("fetchCookies -> response", response);
};
```

9. Let's try again. Awesome! We got an object that has our data! Now we can save the data in `this.cookies`!

```javascript
fetchCookies = async () => {
  const response = await axios.get("http://localhost:8000/cookies");
  this.cookies = response.data;
};
```

10. Our cookies are now coming from the backend! Amazing. We can delete `cookies.js` and the import!

11. Final touches... Set the initial value of `cookies` to an empty array.

12. Since `fetchCookies` will be used to get the array of cookies from the API and store them in `cookieStore`'s `cookies` array, we need to set `fetchCookies` as an `action` in the `constructor`.

```javascript
constructor() {
    makeObservable(this, {
      cookies: observable,
      fetchCookies: action,
      createCookie: action,
      updateCookie: action,
      deleteCookie: action,
    })
  }
```
