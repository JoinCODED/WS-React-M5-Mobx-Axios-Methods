At the moment, `updateCookie` in `cookieStore` updates an existing cookie, but once we refresh our app the cookie is back to its original state. So we need to update the cookie in the backend's database.

1. In `updateCookie`, let's comment out the existing code for now.

```javascript
updateCookie = async (updatedCookie) => {
  // const cookie = this.cookies.find(
  //   (cookie) => cookie.id === updatedCookie.id
  // );
  // for (const key in cookie) cookie[key] = updatedCookie[key];
};
```

2. As we agreed, we add a `try catch` statement whenever we're making an `axios` request.

```javascript
updateCookie = async (updatedCookie) => {
  // const cookie = this.cookies.find(
  //   (cookie) => cookie.id === updatedCookie.id
  // );
  // for (const key in cookie) cookie[key] = updatedCookie[key];
  try {
  } catch (error) {
    console.log("CookieStore -> updateCookie -> error", error);
  }
};
```

3. Make your function asynchronous using `async`.

```javascript
updateCookie = async (updatedCookie) => {};
```

4. Let's make our request! Since we're sending a request to the update endpoint, our `axios` method will be `put`. Don't forget to add `await` before `axios`.

```javascript
try {
  await axios.put();
}
```

5. The update endpoint requires the updated cookie object **and** the ID of the cookie we want to update. The `put` method -like the `post` method- takes two arguments, the endpoint's URL and the cookie object. We will interpolate the updated cookie's ID in the URL and pass `updatedCookie`.

```javascript
try {
  await axios.put(
    `http://localhost:8000/cookies/${updatedCookie.id}`,
    updatedCookie
  );
}
```

6. Since the update cookie endpoint sends no data in the response, we don't need to save it. Now let's try updating the cookie. Nothing happened..

7. Let's refresh the page. The cookie is updated! But why do we need to refresh the page to see the change?! That's because we're updating it in the backend only. And our list of cookies is fetched from the backend when the app first runs only.

8. So we need to update the cookie from the frontend as well. Let's return our commented out code, and call it under the `axios` request.

```javascript
try {
  await axios.put(
    `http://localhost:8000/cookies/${updatedCookie.id}`,
    updatedCookie
  );
  const cookie = this.cookies.find((cookie) => cookie.id === updatedCookie.id);
  for (const key in cookie) cookie[key] = updatedCookie[key];
}
```

10. Try updating another cookie. It works perfectly!
