# InvitableUser

StrongLoop LoopBack based infrastructure for user invitation logic, using Mandrill as email service.

## Files to copy

```
server/boot/roles.js
server/boot/email.js
server/models/invite.json
server/models/invite.js
server/models/invitable_user.json
server/models/invitable_user.js
```


## Files to edit edit

### `.env`

Add to your environmental configuration files the following information:

```
EMAIL_USER=[mandril registration email]
EMAIL_PASS=[mandril secret]
SECRET=[a random string]
```

- - -

### `server/boot/roles.js`

Add your application roles, row 4:

```
var ROLES = ['admin', 'editor', 'author'];
```

and modify your default admin information and credentials, row 6 and followings:

```
var DEFAULT_ADMIN = {
  fullname: 'Main Admin',
  isMainAdmin: true,
  role: 'admin',
  password: '123',
  email: 'admin@x-journal.com'
};
```

- - -

### `server/model-config.json`

Be sure your `AccassToken`, `ACL`, `RoleMapping` and `Role` models are stored onto DB and not public, `Invite`, `Email` and `InvitableUser` or its extension models are configured:

```
"AccessToken": {
  "dataSource": "mongo",
  "public": false
},
"ACL": {
  "dataSource": "mongo",
  "public": false
},
"RoleMapping": {
  "dataSource": "mongo",
  "public": false
},
"Role": {
  "dataSource": "mongo",
  "public": false
},
"Email": {
  "dataSource": "email",
  "public": false
},
"Invite": {
  "dataSource": "mongo"
},
"InvitableUser": {
  "dataSource": mongo"
}
```

- - -

### `server/datasources.json`

Add the email datasource configuration:

```
  "email": {
    "name": "email",
    "connector": "mail",
    "transports": [{
      "type": "smtp",
      "host": "smtp.mandrillapp.com",
      "secure": false,
      "port": 587,
      "tls": {
        "rejectUnauthorized": false
      }
    }]
  }
```

- - -

### `server/config.json`

Be sure that `enableHttpContex` is `true`:

```
"remoting": {
  "context": {
    "enableHttpContext": true
  },
  ...
}
```

- - -

## Clientside available components

On the clientside the following components are available (once `InvitableUser` is extended by `Member` model):

- `admin/page-invite`
- `admin/page-login`
- `admin/page-member`
- `admin/page-settings`
- `admin/page-signup`
- `admin/page-team`
- `admin/part-date`
