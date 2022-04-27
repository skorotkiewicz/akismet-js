An [Akismet](http://www.akismet.com/) API client for [node.js](http://nodejs.org/).

### Installation:

```
yarn add akismet-js
// or
npm i akismet-js
```

### Usage:

You need to [sign up](https://akismet.com/signup/) for an Akismet API key to use the API. Once you sign up,
it would be a good idea to verify your key.

```js
var akismet = require("akismet").client({
  blog: "http://my.blog.com",
  apiKey: "myakismetapikey123",
});

akismet.verifyKey((err, verified) => {
  if (verified) console.log("API key successfully verified.");
  else console.log("Unable to verify API key.");
});
```

You can now use Akismet to moderate your comments.

```js
akismet.checkComment(
  {
    user_ip: "1.1.1.1",
    permalink: "http://www.my.blog.com/my-post",
    comment_author: "spammer",
    comment_content: "spamming your comments",
  },
  (err, spam) => {
    if (spam) console.log("Spam caught.");
    else console.log("Not spam");
  }
);
```

You can also send feedback to Akismet with `submitSpam` and `submitHam`. Their usage is the same as `checkComment`.

```js
akismet.submitSpam(
  {
    user_ip: "1.1.1.1",
    permalink: "http://www.my.blog.com/my-post",
    comment_author: "spammer",
    comment_content: "that was spam but you failed to catch me",
  },
  (err) => {
    console.log("Spam reported to Akismet.");
  }
);
```
