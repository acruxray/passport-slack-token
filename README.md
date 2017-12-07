# Passport-Slack-Token

[Passport](http://passportjs.org/) strategy for authenticating with [Slack](https://slack.com/)  access tokens using the OAuth 2.0 API.

This module lets you authenticate using Slack in your Node.js applications.
By plugging into Passport, Slack authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Installation

```bash
npm install passport-slack-token
```

## Usage

#### Configure Strategy

The Slack authentication strategy authenticates users using a Slack
account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a app ID and app secret.

```javascript
var SlackTokenStrategy = require('passport-slack-token').Strategy;

passport.use(new SlackTokenStrategy({
    clientID: SLACK_CLIENT_ID,
    clientSecret: SLACK_CLIENT_SECRET
  },
  function(accessToken, refreshToken, profile, done) {
    User.findOrCreate({ slackId: profile.id }, function (err, user) {
      return done(err, user);
    });
  }
));
```

#### Authenticate Requests

Use `passport.authenticate('slack-token')` to authenticate requests.

```javascript
router.get('/auth/slack/token', passport.authenticate('slack-token'),
  function(req, res) {
    res.send(req.user);
  });
```

GET request need to have `access_token` and optionally the `refresh_token` in either the query string or set as a header.  If a POST is being preformed they can also be included in the body of the request.

## Credits

* [Rob DiMarco](https://github.com/robertdimarco)
* [Nicholas Penree](https://github.com/drudge)
* [Jared Hanson](https://github.com/jaredhanson)

## License

[MIT License](https://opensource.org/licenses/MIT)

Copyright (c) 2017 Nazar Mozol
