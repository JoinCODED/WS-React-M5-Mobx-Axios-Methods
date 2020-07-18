Since we're fetching data that will be globally accessing by our components, we will create our fetch method in `cookieStore`.

1. We will create a method that sends a request to fetch the cookies from the backend, for now let's console log any message in it:

```javascript
fetchCookies = () => {
  console.log("Let's fetch some cookies");
};
```

2. Now, when do we want to call this method? When the application first starts. We can call it in many places, but the simplest place is right after creating our store instance. We call a method here if we want to run it one time only when the app first runs:

```javascript
const cookieStore = new CookieStore();
cookieStore.fetchCookies();

export default cookieStore;
```

3. Let's check our console. We're getting our message when the app first runs. Try refreshing and you'll see the same result.

