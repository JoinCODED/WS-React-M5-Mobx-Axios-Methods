What if there was an error when fetching? We need to handle it.

1. Let's ruin the URL to create an error

```javascript
fetchCookies = async () => {
  const response = await axios.get("localhost:8000/coies");
  this.cookies = response.data;
};
```

2. The error is not handled. To handle our error we will use a `try catch` statement. In the `try` code block you will put your `axios` code, at any point if an error was caught, the code will break and jump to the `catch` block.

```javascript
fetchCookies = async () => {
  try {
    const response = await axios.get("http://localhost:8000/coies");
    this.cookies = response.data;
  } catch (error) {}
};
```

3. For now, we will only console log our error

```javascript
fetchCookies = async () => {
  try {
    const response = await axios.get("http://localhost:8000/coies");
    this.cookies = response.data;
  } catch (error) {
    console.error("CookieStore -> fetchCookies -> error", error);
  }
};
```
