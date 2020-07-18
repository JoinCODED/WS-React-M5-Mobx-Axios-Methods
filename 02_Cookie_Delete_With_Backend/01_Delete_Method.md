At the moment, `deleteCookie` in `cookieStore` deletes the cookie from our list of cookies, but once we refresh our app the deleted cookie is back. So we need to delete the cookie from the backend's database.

1. In `deleteCookie`, let's comment out the existing code for now.

```javascript
deleteCookie = (cookieId) => {
  // this.cookies = this.cookies.filter((cookie) => cookie.id !== +cookieId)
};
```

2. As we agreed, we add a `try catch` statement whenever we're making an `axios` request.

```javascript
deleteCookie = (cookieId) => {
  // this.cookies = this.cookies.filter((cookie) => cookie.id !== +cookieId)
  try {
  } catch (error) {
    console.log("CookieStore -> deleteCookie -> error", error);
  }
};
```

3. Make your function asynchronous using `async`.

```javascript
deleteCookie = async (cookieId) => {};
```

4. Let's make our request! Since we're sending a request to the delete endpoint, our `axios` method will be `delete`. Don't forget to add `await` before `axios`.

```javascript
try {
  await axios.delete();
}
```

5. The delete request in the backend doesn't return anything, so we don't need to save the response.

6. Now the delete endpoint requires the ID of the cookie we want to delete, so we need to pass it in the URL. So we will use template literals and inject the ID in the URL:

```javascript
try {
  await axios.delete(`http://localhost:8000/cookies/${cookieId}`);
}
```

7. Let's try it out. Hmm.. nothing happened. But we didn't get an error message which means the code inside the `try` block worked perfectly.

8. Let's refresh the page. The cookie is gone! But why do we need to refresh the page to see the change?! That's because we're deleting it from the backend only. And our list of cookies is fetched from the backend when the app first runs only.

9. So we need to delete the cookie from the frontend as well. Let's return our `filter`ing method, and call it under the `axios` request.

```javascript
try {
  await axios.delete(`http://localhost:8000/cookies/${cookieId}`);
  this.cookies = this.cookies.filter((cookie) => cookie.id !== +cookieId);
}
```

10. Try deleting another cookie. It works perfectly!
