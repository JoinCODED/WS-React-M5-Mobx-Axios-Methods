Now that we have 2 methods, fetch and delete, we start to notice that the URL is repeating, and as programars we hate to repeat ourselves!

But Axios has a cool feature called Axios instances, and this is how we are going to use it:

1. Create a file called `instance.js`.
2. Inside this file import Axios.
   ```js
   import axios from 'axios';
   ```
3. Now we will create our instance using the `axios.create` method:
   ```js
   axios.create({
     baseURL: `http://localhost:3000`,
   });
   ```
4. As you see, we took the part that is alwayes the same across our api calls and stored it in this instance. next we have to export this instance:
   ```js
   export default axios.create({
     baseURL: `http://localhost:3000`,
   });
   ```
5. In your store, were you do your api calls, import the instance we just created:
   ```js
   import instance from './instance.js';
   ```
6. Now replace the axios call in the fetch cookie method with our instance:

   ```js
   fetchCookies = async () => {
     try {
       const response = await instance.get('/cookies');
       this.cookies = response.data;
     } catch (error) {
       console.error('CookieStore -> fetchCookies -> error', error);
     }
   };
   ```

   As you see, we don't have to type our full url in the call because we already stored it in the instance!

7. Now do the same for the delete method:

```js
try {
  await instance.delete(`/cookies/${cookieId}`);
  this.cookies = this.cookies.filter((cookie) => cookie.id !== +cookieId);
}
```
