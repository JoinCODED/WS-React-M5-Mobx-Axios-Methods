At the moment, `createCookie` in `cookieStore` creates a cookie and adds it to the list of cookies, but once we refresh our app the new cookie is gone. So we need to create a cookie in the backend's database.

1. In `createCookie`, let's comment out the existing code for now.

```javascript
createCookie = (newCookie) => {
  //   newCookie.id = this.cookies[this.cookies.length - 1].id + 1;
  //   this.cookies.push(newCookie);
};
```

2. As we agreed, we add a `try catch` statement whenever we're making an `axios` request.

```javascript
createCookie = (newCookie) => {
  //   newCookie.id = this.cookies[this.cookies.length - 1].id + 1;
  //   this.cookies.push(newCookie);
  try {
  } catch (error) {
    console.log("CookieStore -> createCookie -> error", error);
  }
};
```

3. Make your function asynchronous using `async`.

```javascript
createCookie = async (newCookie) => {};
```

4. Let's make our request! Since we're sending a request to the create endpoint, our `axios` method will be `post`. Don't forget to add `await` before `axios`.

```javascript
try {
  await axios.post();
}
```

5. The create endpoint requires the new cookie object. The `post` method takes two arguments, the endpoint's URL and the cookie object

```javascript
try {
  const res = await axios.post("http://localhost:8000/cookies", newCookie);
}
```

7. Let's console log the response and try it out. Hmm.. our cookie was not added. But we didn't get an error message which means the code inside the `try` block worked perfectly, and we got the new cookie in the response! It also has the ID!

```javascript
try {
  const res = await axios.post("http://localhost:8000/cookies", newCookie);
  console.log("CookieStore -> createCookie -> res", res);
}
```

8. Let's refresh the page. The new cookie is still there! But why do we need to refresh the page to see the change?! That's because we're creating it in the backend only. And our list of cookies is fetched from the backend when the app first runs only.

9. So we need to create the cookie from the frontend as well. Let's return our `push`, and call it under the `axios` request. But this time, we will pass it the data coming from the response as it has the ID as well. And we don't need to generate the ID in the frontend anymore.

```javascript
try {
  const res = await axios.post("http://localhost:8000/cookies", newCookie);
  this.cookies.push(res.data);
}
```

10. Try creating another cookie. It works perfectly!
