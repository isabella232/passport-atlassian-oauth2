# passport-atlassian-oauth2

[Passport](https://github.com/jaredhanson/passport) strategy for authenticating
with [Atlassian](https://atlassian.com) services using OAuth 2 3LO (three-legged OAuth).

*NOTE: Currently, only Jira supports Atlassian Oauth 2 authorization code grants (3LO).*


## Install
```shell
$ npm install passport-atlassian-oauth2
```

## Usage

#### Create Application

Before using `passport-atlassian-oauth2` you must register an application within [App Management](https://developer.atlassian.com/apps/). If you don't have one follow ["Enabling OAuth 2.0 authorization code grants"](https://developer.atlassian.com/cloud/jira/platform/oauth-2-authorization-code-grants-3lo-for-apps/#enabling-oauth-2-0-authorization-code-grants) instructions from Jira documentation page.

#### Configure Strategy

The client ID and secret obtained when creating an application are supplied as options when creating the strategy.

```js
const AtlassianStrategy = require('passport-atlassian-oauth2');

passport.use(new AtlassianStrategy({
    clientID: '<ATLASSIAN_CLIENT_ID>',
    clientSecret: '<ATLASSIAN_CLIENT_SECRET>',
    callbackURL: 'http://localhost:8080/auth/atlassian/callback',
    scope: 'offline_access read:jira-user',
  },
  (accessToken, refreshToken, profile, cb) => {
    // optionally save profile data to db
    done(null, profile);
  }
));
```

See complete Express.js example [here](https://github.com/jsarafajr/passport-atlassian-oauth2/tree/master/examples/express.js). 

## Sample Profile
```json
{
  "id": "552048:ccc138d6-d39f-1337-93ca-888ff2s05d9e",
  "displayName": "Yevhenii Baraniuk",
  "email": "yevhenii@example.com",
  "photo": "https://avatar-cdn.atlassian.com/21kfjvu62hmkvo3ikdlqo48755?by=hash",
  "provider": "atlassian",
  "accessibleResources": [
    {
      "id": "3942d640-b74e-11e8-96f8-529269fb1459",
      "name": "awesome-jira",
      "scopes": ["read:jira-user"],
      "avatarUrl": "https://site-admin-avatar-cdn.prod.public.atl-paas.net/avatars/240/trophy.png"
    },
    {
      "id": "eff705b1-5cd8-40d1-ac46-9a9516cbc527",
      "name": "super-product",
      "scopes": ["read:jira-user"],
      "avatarUrl": "https://site-admin-avatar-cdn.prod.public.atl-paas.net/avatars/240/cup.png"
    }
  ]
}
```

## License

[The MIT License](http://opensource.org/licenses/MIT)

Copyright (c) 2018 [Yevhenii Baraniuk](http://github.com/jsarafajr)
